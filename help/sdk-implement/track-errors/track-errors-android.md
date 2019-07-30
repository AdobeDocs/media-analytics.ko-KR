---
seo-title: Android에서 오류 추적
title: Android에서 오류 추적
uuid: 7 D 0 C 77 E 5-924 C -4619-8 E 29-3484748 AB 736
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Android에서 오류 추적{#track-errors-on-android}

>[!IMPORTANT]
>
>다음은 모든 2.x SDK에 구현과 관련된 지침입니다. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

1. 미디어 플레이어 오류 추적:

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("mediaErrorID"); 
   }
   ```

>[!NOTE]
>
>미디어 플레이어 오류를 추적해도 미디어 추적 세션이 중지되지 않습니다. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

