---
title: Android에서 체감 품질 추적
description: 이 항목에서는 Android에서 미디어 SDK를 사용하여 QoE, QoS(체감 품질) 추적을 구현하는 방법에 대해 설명합니다.
uuid: 81ff3939-48a6-45c1-8837-dfa3349059
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Android에서 체감 품질 추적{#track-quality-of-experience-on-android}

>[!IMPORTANT]
>
>다음은 모든 2.x SDK에 구현과 관련된 지침입니다. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## QoS 구현

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

   ```java
   MediaObject qosObject =  
     MediaHeartbeat.createQoSObject(<BITRATE>,  
                                    <STARTUP_TIME>,  
                                    <FPS>,  
                                    <DROPPED_FRAMES>);
   ```

1. `getQoSObject()` 메서드가 업데이트된 최신 QoS 정보를 반환하는지 확인합니다.
1. 재생 시 비트율이 변경되면 미디어 하트비트 인스턴스에서 `BitrateChange`를 호출합니다:

   ```java
   public void onBitrateChange(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, null, null); 
   } 
   ```

   >[!IMPORTANT]
   >
   >QoS 개체를 업데이트하고 비트율 변경 시 비트율 변경 이벤트를 호출합니다. 이렇게 하면 가장 정확한 QoS 데이터가 제공됩니다.

