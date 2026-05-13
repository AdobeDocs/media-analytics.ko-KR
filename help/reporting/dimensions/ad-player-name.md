---
title: 광고 플레이어 이름
description: 각 광고를 렌더링한 플레이어를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---


# 광고 플레이어 이름

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**광고 플레이어 이름**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [광고 플레이어 이름](/help/implementation/variables/ads/ad-player-name.md)을 참조하세요.*

>[!ENDSHADEBOX]

**광고 플레이어 이름** 차원은 각 광고를 렌더링한 플레이어를 보고합니다(예: `"Freewheel"`, `"Google IMA"`). 광고가 서버측 광고 삽입 서비스에 의해 에서 결합되는 경우 광고 플레이어는 기본 컨텐츠 플레이어와 다를 수 있습니다.

## 이 차원이 채워지는 방법

광고 플레이어 이름은 `media.adStart` 이벤트마다 플레이어가 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 광고]](/help/reporting/media-reports-enable.md)를 사용하도록 설정한 경우 컨텍스트 데이터 `a.media.ad.playerName`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 데이터 피드 | `videoadplayername, post_videoadplayername` |

## 차원 항목

각 항목은 `media.adStart`에 보고된 리터럴 광고 플레이어 이름입니다.
