---
title: JavaScript 3.x를 사용하여 오류 추적
description: 이 항목에서는 브라우저 앱(JS)에서 Media SDK를 사용하여 오류 추적을 구현하는 방법에 대해 설명합니다.
translation-type: tm+mt
source-git-commit: 5f274452b9ff5770908f7e2e450935be572a22ea
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 69%

---


# JavaScript 3.x를 사용하여 오류 추적{#track-errors-on-javascript}

>[!IMPORTANT]
>
>다음은 모든 3.x SDK에 구현과 관련된 지침입니다. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 오류 추적 구현

1. 미디어 플레이어 오류를 추적합니다.

   ```js
   onPlayerError = function() {
       tracker.trackError("errorId");
   };
   ```

>[!NOTE]
>
>미디어 플레이어 오류를 추적해도 미디어 추적 세션이 중지되지 않습니다. 미디어 플레이어 오류로 인해 재생이 계속되지 않는 경우 `trackError` 호출 후 `trackSessionEnd`를 호출하여 미디어 추적 세션이 종료되었는지 확인하십시오.