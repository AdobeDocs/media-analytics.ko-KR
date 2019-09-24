---
seo-title: JavaScript에서 오류 추적
title: JavaScript에서 오류 추적
uuid: 5a4fc5df-2677-4189-92af-5cd074847b39
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# JavaScript에서 오류 추적{#track-errors-on-javascript}

>[!IMPORTANT]
>
>다음은 모든 2.x SDK에 구현과 관련된 지침입니다. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 오류 추적 구현

1. Track media player errors:

   ```js
   onPlayerError = function() { 
       this._mediaHeartbeat.trackError("mediaErrorId"); 
   };
   ```

>[!NOTE]
>
>미디어 플레이어 오류를 추적해도 미디어 추적 세션이 중지되지 않습니다. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

