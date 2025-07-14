---
title: Chromecast에서 체감 품질을 추적하는 방법에 대해 알아보기
description: Chromecast에서 Media SDK을 사용하여 체감 품질(QoE, QoS) 추적을 구현하는 방법에 대해 알아봅니다.
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
exl-id: 04b9b888-2727-4aa6-a934-94a02c85a490
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 94%

---

# Chromecast에서 체감 품질 추적{#track-quality-of-experience-on-chromecast}

다음은 모든 2.x SDK에 구현과 관련된 지침입니다.

>[!IMPORTANT]
>
>SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/getting-started/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

## 개요 {#overview}

체감 품질 추적에 QoS(서비스 품질) 및 오류 추적이 포함됩니다. 둘 다 선택적 옵션이며 코어 미디어 추적 구현에 필요하지 **않습니다**. 미디어 플레이어 API를 사용하여 QoS 및 오류 추적과 관련된 변수를 식별할 수 있습니다.

## 플레이어 이벤트 {#player-events}

### 모든 비트율 변경 이벤트

* 재생에 대한 QoS 개체 인스턴스 `qosObject` 생성/업데이트
* 호출 `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### 플레이어 오류 시

호출 `trackError("media error id");`

## 구현 {#implement}

1. 미디어 재생 중에 비트율이 변경되는 시점을 식별하고 QoS 정보를 사용하여 `MediaObject` 인스턴스를 만듭니다.

   **QoSObject 변수:**

   >[!TIP]
   >
   >다음 변수는 QoS를 추적하려는 경우에만 필요합니다.

   | 변수 | 설명 | 필수 여부 |
   | --- | --- | :---: |
   | `bitrate` | 현재 비트율 | 예 |
   | `startupTime` | 시작 시간 | 예 |
   | `fps` | FPS 값 | 예 |
   | `droppedFrames` | 드롭된 프레임 수 | 예 |

   **QoS 개체 작성:** [createQoSObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createQoSObject)

   ```
   qosInfo = ADBMobile.media.createQoSObject(50000, 0, 24, 10);
   ```

1. 재생 시 비트율이 변경되면 미디어 하트비트 인스턴스에서 `BitrateChange`를 호출합니다([trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)).

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
   ```

   >[!IMPORTANT]
   >
   >비트율 변경 시마다 QoS 개체를 업데이트하고 비트율 변경 이벤트를 호출합니다. 이렇게 하면 가장 정확한 QoS 데이터가 제공됩니다.

1. `getQoSObject()` 메서드가 업데이트된 최신 QoS 정보를 반환하는지 확인합니다.
1. 미디어 플레이어에 오류가 발생하여 플레이어 API에 오류 이벤트를 사용할 수 있는 경우 `trackError()`를 사용하여 오류 정보를 캡처합니다. ([개요](/help/use-cases/track-errors/track-errors-overview.md)를 참조하십시오.)

   >[!TIP]
   >
   >미디어 플레이어 오류를 추적해도 미디어 추적 세션이 중지되지 않습니다. 미디어 플레이어 오류로 인해 재생이 계속되지 않는 경우 `trackError()` 호출 후 `trackSessionEnd()`를 호출하여 미디어 추적 세션이 종료되었는지 확인하십시오.
