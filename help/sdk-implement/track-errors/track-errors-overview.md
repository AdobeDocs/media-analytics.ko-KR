---
title: 개요
description: Media SDK를 사용한 오류 추적입니다.
uuid: d71429e6-ef8b-4ea2-8491-ff3cdbf4357f
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 개요{#overview}

>[!IMPORTANT]
>
>다음은 모든 2.x SDK에 구현과 관련된 지침입니다. SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/sdk-implement/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

## 오류 추적 구현

1. 미디어 플레이어 오류를 추적합니다.

   오류 이벤트에서 오류 정보로 `trackError`를 호출하십시오.

>[!NOTE]
>
>미디어 플레이어 오류를 추적해도 미디어 추적 세션이 중지되지 않습니다. 미디어 플레이어 오류로 인해 재생이 계속되지 않는 경우 `trackError` 호출 후 `trackSessionEnd`를 호출하여 미디어 추적 세션이 종료되었는지 확인하십시오.

