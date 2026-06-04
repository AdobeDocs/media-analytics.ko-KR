---
title: 평균 분당 시청자
description: 콘텐츠의 런타임 시 주어진 분마다 시청하는 평균 시청자 수를 보고합니다.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 12%

---


# 평균 분당 시청자

**분당 평균 시청 시간** 지표는 콘텐츠의 런타임 동안 주어진 분마다 시청하는 평균 시청자 수를 보고합니다. 다양한 길이의 콘텐츠에서 미디어 도달 범위를 비교하는 데 사용되는 표준 &quot;AMA&quot; 측정입니다.

## 이 지표의 계산 방법

미디어 백엔드는 세션당 분당 평균 시청 시간을 `Content time spent / Content length`(으)로 계산합니다. 세션 간에 합산되면 합계는 콘텐츠의 각 분에서의 평균 대상자 크기를 나타냅니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.averageMinuteAudience`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.averageMinuteAudience`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.averageMinuteAudience` |

>[!IMPORTANT]
>
>분당 평균 시청 시간을 사용하려면 0이 아닌 [콘텐츠 길이](/help/reporting/dimensions/content-length.md)가 필요합니다. 콘텐츠 길이가 설정되지 않았거나 0인 경우 이 지표가 세션에 대해 생성되지 않습니다.
