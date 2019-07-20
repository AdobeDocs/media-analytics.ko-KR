---
seo-title: iOS에서 오류 추적
title: iOS에서 오류 추적
uuid: 18 EA 93 D 3-5948-4375-BCDB -72309268 E 38 D
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# iOS에서 오류 추적{#track-errors-on-ios}

>[!IMPORTANT]
>
>다음은 모든 2.x SDK에 구현과 관련된 지침입니다. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

## 오류 추적 구현

1. 미디어 플레이어 오류 추적:

   ```
   - (void)onPlayerError:(NSNotification *)notification { 
       [_mediaHeartbeat trackError:@"mediaoErrorId"]; 
   }
   ```

>[!NOTE]
>
>미디어 플레이어 오류를 추적해도 미디어 추적 세션이 중지되지 않습니다. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

