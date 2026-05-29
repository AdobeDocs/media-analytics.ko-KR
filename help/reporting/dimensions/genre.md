---
title: 장르
description: 컨텐츠 장르를 보고합니다. 다중 장르 컨텐츠는 라인 항목 간에 분할되며, 각 항목은 동일한 지표 가중치를 받습니다.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---


# 장르

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**장르**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [장르](/help/implementation/variables/standard-metadata/genre.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**장르** 차원은 콘텐츠 장르를 보고합니다. 장르는 쉼표로 구분된 문자열로 수집되고 목록 차원으로 저장됩니다. 다중 장르 컨텐츠는 각각 동일한 지표 가중치를 받는 개별 라인 항목 간에 분할됩니다. 단일 다중 장르 에셋에 소요된 시간을 두 번 계산하지 않고 장르 간에 참여를 비교할 수 있습니다.

## 이 차원이 채워지는 방법

장르는 세션 시작 시 플레이어가 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 비디오 메타데이터]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.genre`에서 자동으로 수집됩니다(목록 변수로 저장됨). |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.genreList`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) 또는 [`xdm.mediaReporting.sessionDetails.genre`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting)&#x200B;(레거시) |
| 데이터 피드 | `videogenre`, `post_videogenre` |
| Audience Manager | `c_contextdata.a.media.genre` |

## 차원 항목

각 항목은 장르 값입니다. 다중 장르 세션(예: `"Drama,Action"`)은 두 개의 개별 라인 항목(`Drama` 및 `Action`)으로 표시되며 각 항목은 세션에 대한 전체 크레딧을 받습니다.
