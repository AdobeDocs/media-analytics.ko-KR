---
title: 시즌
description: 에피소드 콘텐츠에 대한 시즌 번호를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 10%

---


# 시즌

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**시즌**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [시즌](/help/implementation/variables/standard-metadata/season.md)을 참조하세요.*

>[!ENDSHADEBOX]

**시즌** 차원은 에피소드 콘텐츠에 대한 시즌 번호를 보고합니다. 전체 에피소드를 보려면 [표시](show.md) 및 [에피소드](episode.md)와 함께 사용하십시오.

## 이 차원이 채워지는 방법

시즌은 콘텐츠가 시리즈의 일부인 세션 시작 시 플레이어에 의해 설정됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 비디오 메타데이터]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.season`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.season`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videoseason`, `post_videoseason` |
| Audience Manager | `c_contextdata.a.media.season` |

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 시즌 값입니다(일반적으로 `"1"`, `"2"`과(와) 같은 문자열 정수). 동일한 프로그램 내의 에피소드 간에 일관되도록 하십시오. 차원은 `"1"` 및 `"01"`을(를) 동일한 라인 항목으로 정규화하지 않습니다.
