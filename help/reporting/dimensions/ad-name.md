---
title: 광고 이름
description: 사람이 인식할 수 있는 각 광고의 제목을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 6%

---


# 광고 이름

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**광고 이름**보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [광고 이름](/help/implementation/variables/ads/ad-name.md)을 참조하세요.*

>[!ENDSHADEBOX]

**광고 이름** 차원은 각 광고의 사람이 읽을 수 있는 제목을 보고합니다.

## 이 차원이 채워지는 방법

광고 이름은 플레이어가 [광고 시작](/help/implementation/events/ads/ad-start.md) 이벤트마다 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 광고]](/help/reporting/setup/analytics-reporting.md)를 사용하도록 설정한 경우 컨텍스트 데이터 `a.media.ad.friendlyName`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 데이터 피드 | `videoadname`, `post_videoadname` |
| Audience Manager | `c_contextdata.a.media.ad.friendlyName` |

Adobe Analytics에서 이 차원은 **광고 이름(변수)**(`a.media.ad.friendlyName`에서 직접 수집됨)과 **광고 이름**([광고](ad.md) 차원에서 파생된 분류)의 두 가지 방법으로 표시됩니다. 분류를 사용하는 경우 [분류 세트](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)를 사용하여 해당 값을 채우고 유지 관리해야 합니다. **광고 이름(변수)**&#x200B;을 사용하면 분류 유지 관리가 필요하지 않지만 광고 이름과 상위 [광고](ad.md) 차원 간의 보장된 1:1 관계가 손실됩니다. 구현 워크플로에서 가장 잘 지원하는 구성 요소를 사용하십시오.

## 차원 항목

각 항목은 [광고 시작](/help/implementation/events/ads/ad-start.md)에 보고된 리터럴 광고 제목입니다(예: `"Ford F-150"`).
