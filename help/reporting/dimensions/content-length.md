---
title: 콘텐츠 길이
description: 세션 시작 시 설정된 각 미디어 세션의 총 기간(초)을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 6%

---


# 콘텐츠 길이

>[!BEGINSHADEBOX]

*이 페이지는&#x200B;**콘텐츠 길이**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [콘텐츠 길이](/help/implementation/variables/core/content-length.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**콘텐츠 길이** 차원은 세션 시작 시 설정된 각 미디어 세션의 총 기간(초)을 보고합니다. [진행률 마커](/help/reporting/metrics/progress-markers.md) 및 [분당 평균 시청 시간](/help/reporting/metrics/average-minute-audience.md)을 포함한 백엔드 지표를 구동합니다.

## 이 차원이 채워지는 방법

콘텐츠 길이는 세션 시작 시 플레이어가 설정합니다. 보고된 값은 경과된 플레이헤드가 아닌 에셋의 전체 기간(초)입니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.length`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.length`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videolength`, `post_videolength` |
| Audience Manager | `c_contextdata.a.media.length` |

>[!NOTE]
>
>Adobe Analytics에서 이 값은 [콘텐츠](content.md) 차원의 **비디오 길이** 분류에도 해당합니다. 해당 분류를 별도로 채우고 유지 관리할 책임이 있습니다. Customer Journey Analytics은 이 차원을 직접 사용합니다. 원하는 경우 [값 버킷팅](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dataviews/component-settings/value-bucketing)을 사용할 수 있습니다.

>[!IMPORTANT]
>
>컨텐츠 길이가 설정되지 않았거나 0보다 크지 않으면 해당 세션에 대해 진행률 마커 및 분당 평균 시청 시간이 생성되지 않습니다. 알 수 없는 기간이 있는 라이브 스트림의 경우 `86400`을(를) 설정합니다.

## 차원 항목

각 항목은 세션 시작 시 보고되는 리터럴 길이 값(초)입니다.
