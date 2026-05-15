---
title: 외부 오류 ID
description: CDN 오류와 같은 외부 소스의 고유 오류 식별자를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 7%

---


# 외부 오류 ID

**외부 오류 ID** 차원은 플레이어 SDK 외부의 소스에서 고유 오류 식별자(예: CDN 오류)를 보고합니다. 플레이어는 오류 추적 API를 통해 구현 시 코드 또는 ID를 제공해야 합니다. 세션당 여러 개의 오류 ID가 지원됩니다.

## 이 차원이 채워지는 방법

플레이어가 외부 오류 ID를 [오류](/help/implementation/events/error.md) 이벤트의 추적기에 전달합니다. 백엔드는 세션 전체에서 고유 ID를 수집하고 닫기 호출 시 보고합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.externalErrors`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.externalErrors`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `videoqoeextneralerrors` |
| Audience Manager | `c_contextdata.a.media.qoe.externalErrors` |

## 차원 항목

각 항목은 플레이어에서 제공하는 오류 코드 또는 ID입니다. 세션 간에 오류 ID가 올바르게 롤업되도록 구현 간에 안정적인 분류법을 사용하십시오.
