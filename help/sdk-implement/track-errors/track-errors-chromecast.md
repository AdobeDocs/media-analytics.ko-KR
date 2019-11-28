---
title: Chromecast에서 오류 추적
description: 이 항목에서는 Chromecast에서 Media SDK를 사용하여 오류 추적을 구현하는 방법에 대해 설명합니다.
uuid: efa9de8d-c626-4cb6-b46d-108495dd013a
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Chromecast에서 오류 추적{#track-errors-on-chromecast}

>[!IMPORTANT]
>
>다음은 모든 2.x SDK에 구현과 관련된 지침입니다. SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/sdk-implement/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

## 오류 추적 구현

1. 미디어 플레이어 오류를 추적합니다([trackError](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackError)).

   ```
   trackError(errorId)
   ```

>[!NOTE]
>
>미디어 플레이어 오류를 추적해도 미디어 추적 세션이 중지되지 않습니다. 미디어 플레이어 오류로 인해 재생이 계속되지 않는 경우 `trackError` 호출 후 `trackSessionEnd`를 호출하여 미디어 추적 세션이 종료되었는지 확인하십시오.

