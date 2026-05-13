---
title: 광고 URL
description: 각 광고 크리에이티브의 에셋 URL을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 9%

---


# 광고 URL

>[!BEGINSHADEBOX]

*이 페이지는&#x200B;**Creative URL**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [Creative URL](/help/implementation/variables/ads/creative-url.md)을 참조하세요.*

>[!ENDSHADEBOX]

**Creative URL** 차원은 각 광고 크리에이티브의 에셋 URL을 보고합니다. URL 자체가 분석에 의미가 있는 경우(예: CDN 경로 또는 광고 버전 구분) 차원을 사용합니다.

## 이 차원이 채워지는 방법

플레이어가 모든 `media.adStart` 이벤트에 Creative URL을 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | `a.media.ad.creativeURL`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/ko/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 데이터 피드 | `evar1`-`evar250`, `post_evar1`-`post_evar250`(처리 규칙이 `a.media.ad.creativeURL`을(를) 매핑하는 eVar) |

## 차원 항목

각 항목은 `media.adStart`에 보고된 리터럴 URL 문자열입니다.
