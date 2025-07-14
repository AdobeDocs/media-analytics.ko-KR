---
title: Roku에서 오류를 추적하는 방법에 대해 알아보기
description: Roku에서 Media SDK를 사용하여 오류 추적을 구현하는 방법에 대해 알아봅니다.
uuid: 4e0165f9-9169-47ed-9f11-ea8a8778f663
exl-id: 6a6aae4c-60c3-43ea-9954-0bb31f6456f8
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 100%

---

# Roku에서 오류 추적{#track-errors-on-roku}

다음은 모든 2.x SDK에 구현과 관련된 지침입니다.

>[!IMPORTANT]
>
> SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/getting-started/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

## 오류 추적 구현

1. 미디어 플레이어 오류를 추적합니다.

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(),
                               ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>미디어 플레이어 오류를 추적해도 미디어 추적 세션이 중지되지 않습니다. 미디어 플레이어 오류로 인해 재생이 계속되지 않는 경우 `trackError` 호출 후 `trackSessionEnd`를 호출하여 미디어 추적 세션이 종료되었는지 확인하십시오.
