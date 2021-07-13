---
title: JavaScript 2.x를 사용하여 체감 품질 추적 학습
description: '"JavaScript 2.x를 사용하는 브라우저 앱에서 Media SDK를 사용하여 체감 품질(QoE, QoS) 추적을 구현하는 방법에 대해 알아봅니다."'
uuid: 3bc762a2-9706-4b62-aa91-747f461dd13d
exl-id: 5924eba4-15a9-405b-9a05-8a7308ddec47
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 84%

---

# JavaScript 2.x를 사용하여 체감 품질 추적{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>다음은 모든 2.x SDK에 구현과 관련된 지침입니다. SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/sdk-implement/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

## QOS 구현

1. 미디어 재생 중에 비트율이 변경되는 시점을 식별하고 QoS 정보를 사용하여 `MediaObject` 인스턴스를 만듭니다.

   QoSObject 변수:

   >[!TIP]
   >
   >다음 변수는 QoS를 추적하려는 경우에만 필요합니다.

   | 변수 | 설명 | 필수 여부 |
   | --- | --- | :---: |
   | `bitrate` | 현재 비트율 | 예 |
   | `startupTime` | 시작 시간 | 예 |
   | `fps` | FPS 값 | 예 |
   | `droppedFrames` | 드롭된 프레임 수 | 예 |

   QoS 개체 작성:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and  
   // <droppeFrames> with the current playback QoS values.  
   var qosObject = MediaHeartbeat.createQoSObject(<bitrate>,  
                                                  <startuptime>,  
                                                  <fps>,  
                                                  <droppedFrames>);
   ```

1. 재생 시 비트율이 변경되면 미디어 하트비트 인스턴스에서 `BitrateChange`를 호출합니다:

   ```js
   _onBitrateChange = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject);
   };
   ```

   >[!IMPORTANT]
   >
   >비트율 변경 시마다 QoS 개체를 업데이트하고 비트율 변경 이벤트를 호출합니다. 이렇게 하면 가장 정확한 QoS 데이터가 제공됩니다.

1. `getQoSObject()` 메서드가 업데이트된 최신 QoS 정보를 반환하는지 확인합니다.
1. 미디어 플레이어에 오류가 발생하여 플레이어 API에 오류 이벤트를 사용할 수 있는 경우 `trackError()`를 사용하여 오류 정보를 캡처합니다. ([개요](/help/sdk-implement/track-errors/track-errors-overview.md)를 참조하십시오.)

   >[!TIP]
   >
   >미디어 플레이어 오류를 추적해도 미디어 추적 세션이 중지되지 않습니다. 미디어 플레이어 오류로 인해 재생이 계속되지 않는 경우 `trackError()` 호출 후 `trackSessionEnd()`를 호출하여 미디어 추적 세션이 종료되었는지 확인하십시오.
