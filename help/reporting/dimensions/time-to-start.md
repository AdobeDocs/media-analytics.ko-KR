---
title: 시작 시간(차원)
description: 첫 번째 프레임이 렌더링되기 전 경과 시간을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 6%

---


# 시작 시간(차원)

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**시작 시간**차원을 다룹니다. Adobe Analytics은 동일한 `a.media.qoe.timeToStart` 컨텍스트 데이터 변수에서 쌍을 이루는 [시작 시간(지표)](/help/reporting/metrics/time-to-start.md)을 자동으로 채웁니다. Customer Journey Analytics은 차원 또는 지표로 사용할 수 있는 단일 `xdm.mediaReporting.qoeDataDetails.timeToStart` 필드를 노출합니다. 이 변수를 수집하는 방법은 [시작 시간](/help/implementation/variables/quality/time-to-start.md)을 참조하세요.*

>[!ENDSHADEBOX]

**시작 시간** 차원은 세션 시작과 첫 번째 프레임 렌더링 사이의 경과 시간을 보고합니다. 차원을 사용하여 시작 시간 버킷별로 참여를 분류합니다. Adobe은 값을 초 단위로 저장하고 플레이어가 보고하는 밀리초부터 수집 시 전환합니다.

## 이 차원이 채워지는 방법

세션이 시작되기 전에 플레이어가 QoE 개체에 `timeToStart`을(를) 설정합니다. 백엔드가 닫기 호출에 대한 값을 보고합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.timeToStart`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `videoqoetimetostartevar`, `post_videoqoetimetostartevar` |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |

## 차원 항목

각 항목은 닫기 호출에서 보고된 리터럴 시작 시간 값입니다.
