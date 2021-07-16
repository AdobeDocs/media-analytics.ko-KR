---
title: JavaScript 3.x를 사용하여 오류를 추적하는 방법 알아보기
description: 브라우저 앱(JS)에서 Media SDK를 사용하여 오류 추적을 구현하는 방법에 대해 알아봅니다.
exl-id: 3769fc47-fbc4-4498-9d2a-04c88cdd0e83
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 54%

---

# JavaScript 3.x를 사용하여 오류 추적{#track-errors-on-javascript}

다음은 모든 2.x SDK에 구현과 관련된 지침입니다.

>[!IMPORTANT]
>
>SDK의 이전 버전을 구현하는 경우 다음 위치에서 개발자 안내서를 다운로드할 수 있습니다. [SDK 다운로드](/help/sdk-implement/download-sdks.md)

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
