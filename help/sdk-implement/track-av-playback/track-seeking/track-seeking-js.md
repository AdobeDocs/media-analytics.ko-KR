---
seo-title: JavaScript에서 찾기 추적
title: JavaScript에서 찾기 추적
uuid: 089947 FB -8 BAE -4 AE 8-B 215-53793620 EFD 7
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# JavaScript에서 찾기 추적{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>다음은 모든 2.x SDK에 구현과 관련된 지침입니다. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../../sdk-implement/download-sdks.md)

## 찾기 추적 상수

| 상수 이름 | 설명     |
|---|---|
| `SeekStart` | 이동 시작 이벤트 추적을 위한 상수. |
| `SeekComplete` | 이동 완료 이벤트 추적을 위한 상수. |

## 찾기 구현

1. 미디어 플레이어에서 재생 찾기 이벤트를 수신하고, 찾기 시작 이벤트 알림 시 `SeekStart` 이벤트를 사용하여 찾기를 추적합니다.

   ```js
   _onSeekStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
   };
   ```

1. 미디어 플레이어에서 찾기 완료 알림 시 `SeekComplete` 이벤트를 사용하여 찾기 종료를 추적합니다.

   ```js
   _onSeekComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
   };
   ```

자세한 내용은 추적 시나리오 [주 컨텐츠에서 찾기를 사용하여 VOD 재생](../../../sdk-implement/tracking-scenarios/vod-seeking.md)을 참조하십시오.
