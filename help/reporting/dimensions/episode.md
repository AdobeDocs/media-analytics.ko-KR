---
title: 에피소드
description: 시즌 내의 에피소드 번호를 보고합니다.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 12%
---

# 에피소드

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**에피소드**보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [Episode](/help/implementation/variables/standard-metadata/episode.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

**Episode** 차원은 시즌 내의 에피소드 번호를 보고합니다. [표시](show.md) 및 [시즌](season.md)과(와) 함께 사용하여 개별 에피소드 수준에서 참여를 중단하세요.

## 이 차원이 채워지는 방법

세션 시작 시 플레이어에 의해 에피소드가 설정됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 비디오 메타데이터]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.episode`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.episode`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videoepisode`, `post_videoepisode` |
| Audience Manager | `c_contextdata.a.media.episode` |

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 에피소드 값입니다(일반적으로 `"13"`과(와) 같은 문자열 정수). 에피소드 번호만 계절에 따라 다르지 않습니다. 명확하게 눈에 띄는 부분은 시즌과 함께 사용하십시오.
