---
title: Pod 위치의 광고
description: 상위 광고 브레이크 내에 있는 각 광고의 인덱싱된 위치를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 7%

---


# Pod 위치의 광고

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**Pod 위치의 광고**보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [Pod의 광고 위치](/help/implementation/variables/ads/ad-in-pod-position.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**Pod의 광고 위치** 차원은 상위 광고 브레이크 내에 있는 각 광고의 인덱싱된 위치를 보고합니다. Pod의 첫 번째 광고는 `0`이고 두 번째 광고는 `1`입니다. 차원을 사용하여 광고 브레이크 내에서 위치별로 참여 및 완료를 비교합니다.

## 이 차원이 채워지는 방법

플레이어가 [광고 시작](/help/implementation/events/ads/ad-start.md) 이벤트마다 pod의 광고를 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 광고]](/help/reporting/media-reports-enable.md)를 사용하도록 설정한 경우 컨텍스트 데이터 `a.media.ad.podPosition`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.podPosition`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 데이터 피드 | `videoadinpod`, `post_videoadinpod` |
| Audience Manager | `c_contextdata.a.media.ad.podPosition` |

## 차원 항목

각 항목은 정수 위치 값(`0`, `1`, `2`, ...)입니다. [광고 시작](/help/implementation/events/ads/ad-start.md)에 보고되었습니다.
