---
title: MVPD
description: 사용자가 인증한 케이블, 위성 또는 가상 공급자를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 9%

---


# MVPD

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**MVPD**보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [MVPD](/help/implementation/variables/standard-metadata/mvpd.md)을 참조하세요.*

>[!ENDSHADEBOX]

**MVPD**(다중 채널 비디오 프로그래밍 배포자) 차원은 사용자가 Adobe Pass을 통해 인증한 공급자를 보고합니다(예: `"Comcast"` 또는 `"DirecTV"`). 인증 공급자에 의한 참여를 중단하는 데 사용합니다.

## 이 차원이 채워지는 방법

MVPD은 콘텐츠가 Adobe Pass 뒤에서 게이팅될 때 세션 시작 시 플레이어에 의해 설정됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 비디오 메타데이터]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.pass.mvpd`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.mvpd`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videomvpd`, `post_videomvpd` |
| Audience Manager | `c_contextdata.a.media.pass.mvpd` |

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 MVPD 이름입니다. 공급자별 표준 Adobe Pass MVPD 식별자를 사용하여 데이터가 공급자별 단일 라인 항목으로 롤업되도록 합니다.
