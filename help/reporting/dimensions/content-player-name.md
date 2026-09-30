---
title: 컨텐츠 플레이어 이름
description: 각 미디어 세션을 렌더링한 플레이어를 보고합니다.
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
source-wordcount: '196'
ht-degree: 7%
---

# 컨텐츠 플레이어 이름

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**콘텐츠 플레이어 이름**보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [콘텐츠 플레이어 이름](/help/implementation/variables/core/content-player-name.md)을 참조하세요.*

>[!ENDSHADEBOX]

**콘텐츠 플레이어 이름** 차원은 각 미디어 세션을 렌더링한 플레이어를 보고합니다(예: `HTML5 Player`, `Brightcove` 또는 `Roku Player`). 이를 사용하여 동일한 속성의 플레이어 간 참여, 완료 및 품질을 비교할 수 있습니다.

## 이 차원이 채워지는 방법

플레이어 이름은 세션 시작 시 플레이어가 설정하며 세션 기간 동안 지속됩니다. 이 값은 모든 이벤트에 전송되고 Adobe Analytics 및 Customer Journey Analytics 모두에서 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.playerName`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videoplayername`, `post_videoplayername` |
| Audience Manager | `c_contextdata.a.media.playerName` |

>[!IMPORTANT]
>
>플레이어 이름이 설정되지 않으면 해당 세션에 대한 차원이 채워지지 않습니다. 플레이어 이름이 없는 세션은 보고에서 플레이어별로 분류할 수 없습니다.

## 차원 항목

각 항목은 세션 시작 시 설정된 리터럴 문자열입니다. 다른 플레이어의 데이터가 단일 라인 항목으로 축소되지 않도록 플레이어별로 안정적이고 고유한 이름을 사용합니다.
