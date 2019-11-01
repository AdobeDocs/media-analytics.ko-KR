---
title: Roku에서 오류 추적
description: 이 항목에서는 Roku에서 Media SDK를 사용하여 오류 추적을 구현하는 방법에 대해 설명합니다.
uuid: 4e0165f9-9169-47ed-9f11-ea8a8778f663
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Roku에서 오류 추적{#track-errors-on-roku}

>[!IMPORTANT]
>
>다음은 모든 2.x SDK에 구현과 관련된 지침입니다. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 오류 추적 구현

1. 미디어 플레이어 오류 추적:

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(), 
                               ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>미디어 플레이어 오류를 추적해도 미디어 추적 세션이 중지되지 않습니다. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

