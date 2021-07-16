---
title: Android에서 버퍼링을 추적하는 방법 알아보기
description: Android에서 버퍼링 이벤트를 추적하는 방법을 알아봅니다.
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
exl-id: fcea2ef8-53c5-41fb-8b70-06599c2d9cbf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 87%

---

# Android에서 버퍼링 추적{#track-buffering-on-android}

다음은 모든 2.x SDK에 구현과 관련된 지침입니다.

>[!IMPORTANT]
>SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/sdk-implement/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

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
