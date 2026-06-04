---
title: 광고 로드
description: 각 스트리밍 미디어 세션에 사용되는 광고 로드 유형을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 7%

---


# 광고 로드

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**광고 로드**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [광고 로드 유형](/help/implementation/variables/standard-metadata/ad-load-type.md)을 참조하세요.*

>[!ENDSHADEBOX]

**광고 로드** 차원은 각 스트리밍 미디어 세션의 시작 시 로드된 광고 유형을 보고합니다. 값은 고객이 정의한 값으로, 조직에서 해당 광고 게재 메커니즘(예: `"linear"`, `"dynamic"` 또는 `"programmatic"`)에 따라 세션을 분류할 수 있습니다.

## 이 차원이 채워지는 방법

광고 로드 유형은 세션 시작 시 플레이어가 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 스트리밍 미디어]](/help/reporting/setup/analytics-reporting.md)이(가) 구성되면 컨텍스트 데이터 `a.media.adLoad`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adLoad`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videoadload`, `post_videoadload` |
| Audience Manager | `c_contextdata.a.media.adLoad` |

## 차원 항목

각 항목은 세션 시작 시 설정된 리터럴 광고 로드 유형 문자열입니다. 값은 표준 열거형으로 제한되지 않습니다. 보고서에서 값이 예측 가능하게 롤업되도록 구현 간에 일관된 분류법을 정의합니다.
