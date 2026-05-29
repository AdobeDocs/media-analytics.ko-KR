---
title: 광고
description: 광고 ID로 키로 재생되는 각 고유 광고를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 7%

---


# 광고

>[!BEGINSHADEBOX]

*이 페이지는&#x200B;**광고**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [광고 ID](/help/implementation/variables/ads/ad-id.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**광고** 차원은 [광고 시작](/help/implementation/events/ads/ad-start.md)에 설정된 광고 ID로 키로 재생되는 각 고유 광고를 보고합니다. 차원은 광고 보고를 위한 기본 분류이고 광고 이름, 광고 길이 및 Creative ID와 같은 광고 수준 분류에 대한 조인 키입니다.

## 이 차원이 채워지는 방법

광고는 플레이어가 모든 [광고 시작](/help/implementation/events/ads/ad-start.md) 이벤트에서 광고의 안정적인 식별자로 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 광고]](/help/reporting/media-reports-enable.md)를 사용하도록 설정한 경우 컨텍스트 데이터 `a.media.ad.name`에서 자동으로 수집됩니다. 방문 기간 동안 지속됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 데이터 피드 | `videoad`, `post_videoad` |
| Audience Manager | `c_contextdata.a.media.ad.name` |

>[!IMPORTANT]
>
>광고 ID는 필수입니다. 설정이 해제되었거나 비어 있는 경우 스트리밍 미디어 광고 보고에서 광고가 삭제됩니다.

## 차원 항목

각 항목은 [광고 시작](/help/implementation/events/ads/ad-start.md)에 보고된 고유한 광고 ID입니다. 동일한 광고가 세션 간 단일 라인 항목으로 롤업되도록 크리에이티브당 안정적인 식별자를 사용합니다.
