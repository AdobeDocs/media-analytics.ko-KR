---
seo-title: Android에서 버퍼링 추적
title: Android에서 버퍼링 추적
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Android에서 버퍼링 추적{#track-buffering-on-android}

>[!IMPORTANT]
>다음은 모든 2.x SDK에 구현과 관련된 지침입니다. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDks.](/help/sdk-implement/download-sdks.md)

## 버퍼링 추적 상수

| 상수 이름 | 설명     |
|---|---|
| `MediaHeartbeat.Event.BufferStart` | 버퍼 시작 이벤트 추적을 위한 상수 |
| `MediaHeartbeat.Event.BufferComplete` | 버퍼 완료 이벤트 추적을 위한 상수 |

## 버퍼링 구현

1. 미디어 플레이어에서 재생 버퍼링 이벤트를 수신하고, 버퍼 시작 이벤트 알림 시 `BufferStart` 이벤트를 사용하여 버퍼링을 추적합니다.

   ```java
   public void onBufferStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null); 
   }
   ```

1. 미디어 플레이어에서 버퍼 완료 알림 시 `BufferComplete` 이벤트를 사용하여 버퍼링 종료를 추적합니다.

   ```java
   public void onBufferComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null); 
   }
   ```

자세한 내용은 추적 시나리오 [버퍼링이 있는 VOD 재생](/help/sdk-implement/tracking-scenarios/vod-buffering.md)을 참조하십시오.
