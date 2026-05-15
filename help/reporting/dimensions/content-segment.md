---
title: 컨텐츠 세그먼트
description: 세션 중에 본 플레이헤드 범위를 분 단위로 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 6%

---


# 컨텐츠 세그먼트

**콘텐츠 세그먼트** 차원은 세션 중에 본 플레이헤드 범위를 분 단위로 보고합니다(예: 0-5분 동안 `[0-5]`). 백엔드는 재생 중에 보고된 최소 및 최대 플레이헤드 값에서 세그먼트를 계산합니다. [콘텐츠 세그먼트 보기 수](/help/reporting/metrics/content-segment-views.md) 지표와 함께 사용하여 긴 형식의 콘텐츠 뷰어에서 실제로 사용하는 부분을 분석하십시오.

## 이 차원이 채워지는 방법

컨텐츠 세그먼트는 미디어 백엔드에 의해 세션의 이벤트에 보고된 플레이헤드 값에서 계산됩니다. 클라이언트가 설정하지 않습니다. 보고된 값은 재생 중에 표시되는 플레이헤드 값에서 파생됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.segment`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.segment`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videosegment`, `post_videosegment` |
| Audience Manager | `c_contextdata.a.media.segment` |

>[!IMPORTANT]
>
>세션 중에 플레이헤드가 올바르게 보고되지 않으면 계산된 세그먼트가 부정확할 수 있습니다. 라이브 스트림의 경우 세그먼트는 세션 중에 표시된 상대적 플레이헤드 값에서 계산됩니다.

## 차원 항목

각 항목은 세션 중에 표시되는 플레이헤드 값을 포함하는 문자열 범위입니다(예: `[0-5]`, `[5-10]`, `[10-15]`). 세부 기간은 5분으로 고정됩니다.
