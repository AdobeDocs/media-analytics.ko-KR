---
seo-title: JavaScript에서 체감 품질 추적
title: JavaScript에서 체감 품질 추적
uuid: 3bc762a2-9706-4b62-aa91-747f461dd13d
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# JavaScript에서 체감 품질 추적{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>다음은 모든 2.x SDK에 구현과 관련된 지침입니다. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## QOS 구현

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   QoSObject 변수:

   >[!TIP]
   >
   >이러한 변수는 QoS를 추적하려는 경우에만 필요합니다.

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
   >QoS 개체를 업데이트하고 비트율 변경 시 비트율 변경 이벤트를 호출합니다. 이렇게 하면 가장 정확한 QoS 데이터가 제공됩니다.

1. `getQoSObject()` 메서드가 업데이트된 최신 QoS 정보를 반환하는지 확인합니다.
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (See [Overview](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >미디어 플레이어 오류를 추적해도 미디어 추적 세션이 중지되지 않습니다. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

