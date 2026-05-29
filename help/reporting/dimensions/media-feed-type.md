---
title: 미디어 피드 유형
description: '동일한 콘텐츠가 여러 피드를 통해 전달될 때 브로드캐스트 피드(예: East-HD 또는 West-SD)를 보고합니다.'
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 7%

---


# 미디어 피드 유형

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**미디어 피드 유형**보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [미디어 피드 유형](/help/implementation/variables/standard-metadata/media-feed-type.md)을 참조하세요.*

>[!ENDSHADEBOX]

**미디어 피드 유형** 차원은 각 세션에 대한 브로드캐스트 피드를 보고합니다(예: `"East-HD"`, `"West-SD"` 또는 `"4K"`). 동일한 콘텐츠가 여러 지역 또는 품질 피드를 통해 전달되고 피드당 참여를 보고해야 할 때 사용합니다.

## 이 차원이 채워지는 방법

미디어 피드 유형은 세션 시작 시 플레이어가 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 비디오 메타데이터]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.feed`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.feed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videofeedtype`, `post_videofeedtype` |
| Audience Manager | `c_contextdata.a.media.feed` |

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 피드 값입니다. 지역 또는 품질 분할당 안정적인 피드 식별자 세트를 사용합니다.
