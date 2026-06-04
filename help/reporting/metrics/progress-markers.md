---
title: 진행률 마커
description: 플레이헤드가 5개의 고정된 임계값(10%, 25%, 50%, 75% 및 95%)을 각각 넘은 세션을 카운트합니다.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 9%

---


# 진행률 마커

**진행률 마커**&#x200B;는 플레이헤드가 5개의 고정된 임계값(콘텐츠 길이의 10%, 25%, 50%, 75% 및 95%)을 각각 초과하는 세션을 계산하는 5개의 개별 지표입니다. 이 차트를 사용하여 콘텐츠 런타임 전체에 걸쳐 드롭다운을 차트로 표시합니다. [콘텐츠 시작](content-starts.md)과(와) 연결하여 각 이정표에 도달한 시작된 세션의 공유를 계산합니다.

각 마커는 세션당 한 번 실행되며 검색 시 재시도되지 않습니다. 앞으로 탐색할 때 건너뛴 마커는 카운트되지 않습니다(예: 5%에서 60%로 이동하는 뷰어는 10%, 25% 및 50% 마커를 한 번에 모두 트리거함).

## 각 마커 계산 방법

미디어 백엔드는 각 이벤트 후에 [콘텐츠 길이](../dimensions/content-length.md)에 대해 보고된 플레이헤드를 평가합니다. 플레이헤드가 먼저 임계값을 넘으면 해당 플래그가 세션의 나머지 부분에 대해 설정됩니다. 5개의 마커 모두 근접 호출 시 보고됩니다. 기본 콘텐츠에서 재생 이벤트를 생성하지 않는 세션(예: [시작 전 드롭](/help/reporting/metrics/drops-before-start.md))은 재생 헤드를 임계값을 초과하지 않으므로 마커가 설정되지 않습니다.

>[!IMPORTANT]
>
>진행률 마커에는 0이 아닌 [콘텐츠 길이](/help/reporting/dimensions/content-length.md)와 정확한 플레이헤드 보고가 필요합니다. 컨텐츠 길이가 설정되지 않았거나 0이거나 잘못된 경우 마커가 잘못된 시간에 실행되거나 전혀 실행되지 않을 수 있습니다.

### 10% 진행률 마커 {#progress-10}

플레이헤드가 처음 콘텐츠 길이의 10%에 도달하면 실행됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.progress10`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress10`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.progress10` |

### 25% 진행률 마커 {#progress-25}

플레이헤드가 처음 콘텐츠 길이의 25%에 도달하면 실행됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.progress25`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress25`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.progress25` |

### 50% 진행률 마커 {#progress-50}

플레이헤드가 처음 콘텐츠 길이의 50%에 도달하면 실행됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.progress50`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress50`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.progress50` |

### 75% 진행률 마커 {#progress-75}

플레이헤드가 처음 콘텐츠 길이의 75%에 도달하면 실행됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.progress75`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress75`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.progress75` |

### 95% 진행률 마커 {#progress-95}

플레이헤드가 처음 콘텐츠 길이의 95%에 도달하면 실행됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.progress95`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress95`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.progress95` |
