---
title: JavaScript 2.x를 사용하여 오류 추적
description: 이 항목에서는 브라우저 앱(JS)에서 Media SDK를 사용하여 오류 추적을 구현하는 방법에 대해 설명합니다.
uuid: 5a4fc5df-2677-4189-92af-5cd074847b39
translation-type: tm+mt
source-git-commit: fa161e2d41629fdfe77100d87d6a44728e23d77f
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 89%

---


# JavaScript 2.x를 사용하여 오류 추적{#track-errors-on-javascript}

>[!IMPORTANT]
>
>다음은 모든 2.x SDK에 구현과 관련된 지침입니다. SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/sdk-implement/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

## 오류 추적 구현

1. 미디어 플레이어 오류를 추적합니다.

   ```js
   onPlayerError = function() {
       this._mediaHeartbeat.trackError("mediaErrorId");
   };
   ```

>[!NOTE]
>
>미디어 플레이어 오류를 추적해도 미디어 추적 세션이 중지되지 않습니다. 미디어 플레이어 오류로 인해 재생이 계속되지 않는 경우 `trackError` 호출 후 `trackSessionEnd`를 호출하여 미디어 추적 세션이 종료되었는지 확인하십시오.