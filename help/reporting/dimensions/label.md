---
title: 레이블
description: 오디오 콘텐츠를 릴리스한 레코드 레이블을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 9%

---


# 레이블

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**레이블**보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [Label](/help/implementation/variables/standard-metadata/label.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

**Label** 차원은 오디오 콘텐츠를 릴리스한 레코드 레이블을 보고합니다(예: `"Capitol Records"`). 음악 또는 팟캐스트 카탈로그의 레이블에 대한 참여를 비교할 때 사용합니다.

## 이 차원이 채워지는 방법

레이블은 오디오 콘텐츠에 대한 세션 시작 시 플레이어가 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 오디오 메타데이터]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.label`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.label`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videoaudiolabel` |

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 레이블 이름입니다. 맞춤법 또는 노출 변형 간에 참여가 조각화되지 않도록 레이블당 안정적인 정식 이름을 사용합니다.
