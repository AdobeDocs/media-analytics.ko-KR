---
title: 미디어 경로
description: 콘텐츠 ID를 경로 분석을 위한 트래픽 변수로 캡처합니다.
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
source-wordcount: '219'
ht-degree: 6%
---

# 미디어 경로

**미디어 경로** 차원은 콘텐츠 ID를 트래픽 변수(prop)로 캡처하므로 경로 지정 분석(예: 다음 콘텐츠 및 이전 콘텐츠 흐름 보고서)에 사용할 수 있습니다. Adobe Analytics에 고유합니다. Customer Journey Analytics은 트래픽 변수를 저장하지 않으며, 컨텐츠(ID) 차원에서 직접 경로 지정을 수행합니다.

## 이 차원이 채워지는 방법

미디어 경로는 세션 시작 시 설정된 콘텐츠 ID에서 자동으로 파생됩니다. 설정할 별도의 변수가 없습니다. 컨텐츠(ID)가 채워질 때마다 데이터 피드 열 `videopath`이(가) 채워집니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.name`에서 트래픽 변수(prop)로 자동으로 수집됩니다. |
| Customer Journey Analytics | 해당 없음 — 경로 분석에 [컨텐츠](content.md)를 사용합니다. |
| 데이터 피드 | `videopath`, `post_videopath` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!NOTE]
>
>Adobe Analytics prop에는 100바이트 제한이 있습니다. 100바이트보다 긴 값은 잘립니다.

>[!IMPORTANT]
>
>경로 지정 보고서는 동일한 방문 내의 히트 간에 prop 값을 비교합니다. 방문 내에서 콘텐츠(ID)가 변경되는 경우(예: 뷰어가 한 콘텐츠에서 다른 콘텐츠로 이동하는 경우) 경로 보고서에 해당 흐름이 표시됩니다.

## 차원 항목

각 항목은 방문 중에 보고된 콘텐츠 ID입니다. 흐름 패널을 사용하여 콘텐츠 간 탐색 경로를 볼 수 있습니다.
