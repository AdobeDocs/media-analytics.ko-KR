---
title: Android에서 체감 품질을 추적하는 방법에 대해 알아보기
description: Android에서 Media SDK을 사용하여 체감 품질(QoE, QoS) 추적을 구현하는 방법에 대해 알아봅니다.
uuid: 81ff3939-48a6-45c1-8837-ddfa33490559
exl-id: cee8b119-bca2-4a5c-8111-2b49f7eede66
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 89%

---

# Android에서 체감 품질 추적{#track-quality-of-experience-on-android}

다음은 모든 2.x SDK에 구현과 관련된 지침입니다.

>[!IMPORTANT]
>
>SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/getting-started/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

## QoS 구현

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

   ```java
   MediaObject qosObject =  
     MediaHeartbeat.createQoSObject(<BITRATE>,  
                                    <STARTUP_TIME>,  
                                    <FPS>,  
                                    <DROPPED_FRAMES>);
   ```

1. `getQoSObject()` 메서드가 업데이트된 최신 QoS 정보를 반환하는지 확인합니다.
1. 재생 시 비트율이 변경되면 미디어 하트비트 인스턴스에서 `BitrateChange`를 호출합니다.

   ```java
   public void onBitrateChange(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, null, null);
   }
   ```

   >[!IMPORTANT]
   >
   >비트율 변경 시마다 QoS 개체를 업데이트하고 비트율 변경 이벤트를 호출합니다. 이렇게 하면 가장 정확한 QoS 데이터가 제공됩니다.
