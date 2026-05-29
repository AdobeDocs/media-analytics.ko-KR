---
title: 오류
description: 세션당 오류 이벤트 수를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 6%

---


# 오류

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**오류**차원을 다룹니다. Adobe Analytics은 동일한 `a.media.qoe.errorCount` 컨텍스트 데이터 변수에서 쌍을 이루는 [오류 이벤트 지표](/help/reporting/metrics/error-events.md)을 자동으로 채웁니다. Customer Journey Analytics은 차원 또는 지표로 사용할 수 있는 단일 `xdm.mediaReporting.qoeDataDetails.errorCount` 필드를 노출합니다.*

>[!ENDSHADEBOX]

**오류** 차원은 세션 중에 받은 오류 이벤트의 수를 보고합니다. 차원을 사용하여 정확한 오류 수별로 참여를 분류합니다.

## 이 차원이 채워지는 방법

미디어 백엔드는 플레이어가 보고한 모든 오류에 대한 카운트를 증가시킵니다. 이 값은 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.errorCount`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `videoqoeerrorcountevar`, `post_videoqoeerrorcountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.errorCount` |

## 차원 항목

각 항목은 닫기 호출에서 보고된 리터럴 오류-수 값입니다. 세션 수준 부울 보고(오류가 전혀 발생했는지 여부)의 경우 [오류 영향을 받은 스트림](/help/reporting/metrics/error-impacted-streams.md)을 사용하십시오. 고유 오류 ID의 경우 [외부 오류 ID](external-error-ids.md) 및 [플레이어 SDK 오류 ID](player-sdk-error-ids.md)을(를) 사용하십시오.

>[!NOTE]
>
>이전 하트비트 SDK(미디어 SDK 1.5.x-2.x)를 사용하는 경우, SDK에서 내부적으로 생성된 오류 ID는 컨텍스트 데이터 키 `a.media.qoe.mediaSdkErrors`에서 자동으로 수집되고 사용자 지정 처리 규칙을 통해 Adobe Analytics에서 액세스할 수 있습니다. Audience Manager 트레이트는 `c_contextdata.a.media.qoe.mediaSdkErrors`입니다. 이 필드는 Media Collection API 또는 Media Edge API 구현에 적용할 수 없습니다.
