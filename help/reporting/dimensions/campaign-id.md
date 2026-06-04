---
title: 캠페인 ID
description: 각 광고가 속한 캠페인을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 13%

---


# 캠페인 ID

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**캠페인 ID**보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [캠페인 ID](/help/implementation/variables/ads/campaign-id.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

**캠페인 ID** 차원은 각 광고 크리에이티브가 속한 광고 캠페인을 보고합니다. 차원을 사용하여 캠페인을 공유하는 여러 크리에이티브 간에 참여를 롤업할 수 있습니다.

## 이 차원이 채워지는 방법

플레이어가 [광고 시작](/help/implementation/events/ads/ad-start.md) 이벤트마다 캠페인 ID를 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 광고]](/help/reporting/setup/analytics-reporting.md)를 사용하도록 설정한 경우 컨텍스트 데이터 `a.media.ad.campaign`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 데이터 피드 | `videocampaign`, `post_videocampaign` |
| Audience Manager | `c_contextdata.a.media.ad.campaign` |

## 차원 항목

각 항목은 [광고 시작](/help/implementation/events/ads/ad-start.md)에 보고된 리터럴 캠페인 값입니다.
