---
title: 게재위치 ID
description: 각 광고의 배치 식별자를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 10%

---


# 게재위치 ID

>[!BEGINSHADEBOX]

*이 페이지는&#x200B;**배치 ID**보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [배치 ID](/help/implementation/variables/ads/placement-id.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**배치 ID** 차원은 광고 배치 식별자(일반적으로 광고 서버 플랫폼에 정의된 슬롯 또는 영역)를 보고합니다. 차원을 사용하여 배치 슬롯 간의 참여와 완료를 비교할 수 있습니다.

## 이 차원이 채워지는 방법

플레이어가 [광고 시작](/help/implementation/events/ads/ad-start.md) 이벤트마다 배치 ID를 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | `a.media.ad.placement`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.placementID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 데이터 피드 | `evar1`-`evar250`, `post_evar1`-`post_evar250`(처리 규칙이 `a.media.ad.placement`을(를) 매핑하는 eVar) |
| Audience Manager | `c_contextdata.a.media.ad.placement` |

## 차원 항목

각 항목은 [광고 시작](/help/implementation/events/ads/ad-start.md)에 보고된 리터럴 배치 값입니다.
