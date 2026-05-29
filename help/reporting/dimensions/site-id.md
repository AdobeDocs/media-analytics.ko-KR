---
title: 사이트 ID
description: 각 광고에 대한 광고 사이트 식별자를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 10%

---


# 사이트 ID

>[!BEGINSHADEBOX]

*이 페이지는&#x200B;**사이트 ID**보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [사이트 ID](/help/implementation/variables/ads/site-id.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**사이트 ID** 차원은 광고 사이트 식별자(일반적으로 광고 서버 플랫폼의 ID)를 보고합니다. 차원을 사용하여 광고 배치 사이트별로 참여를 분류합니다.

## 이 차원이 채워지는 방법

플레이어가 [광고 시작](/help/implementation/events/ads/ad-start.md) 이벤트마다 사이트 ID를 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | `a.media.ad.site`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.siteID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 데이터 피드 | `evar1`-`evar250`, `post_evar1`-`post_evar250`(처리 규칙이 `a.media.ad.site`을(를) 매핑하는 eVar) |
| Audience Manager | `c_contextdata.a.media.ad.site` |

## 차원 항목

각 항목은 [광고 시작](/help/implementation/events/ads/ad-start.md)에 보고된 리터럴 사이트 ID 값입니다.
