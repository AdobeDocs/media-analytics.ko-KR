---
title: 광고주
description: 각 광고에 출연한 회사 또는 브랜드를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 12%

---


# 광고주

>[!BEGINSHADEBOX]

*이 페이지는&#x200B;**Advertiser**보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [Advertiser](/help/implementation/variables/ads/advertiser.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**Advertiser** 차원은 각 광고에 포함된 회사 또는 브랜드를 보고합니다(예: `"Ford"` 또는 `"Coca-Cola"`). 차원을 사용하여 광고주별 참여 및 완료를 분류할 수 있습니다.

## 이 차원이 채워지는 방법

광고주는 플레이어가 [광고 시작](/help/implementation/events/ads/ad-start.md) 이벤트마다 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 광고]](/help/reporting/media-reports-enable.md)를 사용하도록 설정한 경우 컨텍스트 데이터 `a.media.ad.advertiser`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 데이터 피드 | `videoadvertiser`, `post_videoadvertiser` |
| Audience Manager | `c_contextdata.a.media.ad.advertiser` |

## 차원 항목

각 항목은 [광고 시작](/help/implementation/events/ads/ad-start.md)에 보고된 리터럴 광고주 이름입니다.
