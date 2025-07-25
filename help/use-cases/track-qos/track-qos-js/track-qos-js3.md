---
title: JavaScript 3.x를 사용하여 체감 품질을 추적하는 방법에 대해 알아보기
description: JavaScript 3x를 사용하는 브라우저 앱에서 Media SDK을 사용하여 체감 품질(QoE, QoS) 추적을 구현하는 방법에 대해 알아봅니다.
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 90%

---

# JavaScript 3.x를 사용하여 체감 품질 추적{#track-quality-of-experience-on-javascript}

다음은 모든 2.x SDK에 구현과 관련된 지침입니다.

>[!IMPORTANT]
>
>SDK의 이전 버전을 구현하는 경우, [SDK 다운로드](/help/getting-started/download-sdks.md)에서 개발자 안내서를 다운로드할 수 있습니다.

## QOE 구현

1. 미디어 재생 중에 비트율이 변경되는 시점을 식별하고 QoE 정보를 사용하여 `qoeObject` 인스턴스를 만듭니다.

   QoEObject 변수:

   >[!TIP]
   >
   >다음 변수는 QoS를 추적하려는 경우에만 필요합니다.

   | 변수 | 유형 | 설명 |
   | --- | --- | --- |
   | `bitrate` | 숫자 | 현재 비트율 |
   | `startupTime` | 숫자 | 시작 시간 |
   | `fps` | 숫자 | FPS 값 |
   | `droppedFrames` | 숫자 | 드롭된 프레임 수 |

   QoE 개체 작성:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
   tracker.updateQoEObject(qoeObject);
   ```

1. 재생 시 비트율이 변경되면 미디어 하트비트 인스턴스에서 `BitrateChange`를 호출합니다.

   ```js
   _onBitrateChange = function() {
       // If the new bitrate value is available provide it to the tracker.
       var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
       tracker.updateQoEObject(qoeObject);
   
       tracker.trackEvent(ADB.Media.Event.BitrateChange);
   };
   ```

   >[!IMPORTANT]
   >
   >비트율 변경 시마다 QoE 개체를 업데이트하고 비트율 변경 이벤트를 호출합니다. 이렇게 하면 가장 정확한 QoE 데이터가 제공됩니다.

1. 최신 QoE 정보를 SDK에 제공하려면 `updateQoEObject()` 메서드를 호출해야 합니다.
1. 미디어 플레이어에 오류가 발생하여 플레이어 API에 오류 이벤트를 사용할 수 있는 경우 `trackError()`를 사용하여 오류 정보를 캡처합니다. ([개요](/help/use-cases/track-errors/track-errors-overview.md)를 참조하십시오.)

   >[!TIP]
   >
   >미디어 플레이어 오류를 추적해도 미디어 추적 세션이 중지되지 않습니다. 미디어 플레이어 오류로 인해 재생이 계속되지 않는 경우 `trackError()` 호출 후 `trackSessionEnd()`를 호출하여 미디어 추적 세션이 종료되었는지 확인하십시오.
