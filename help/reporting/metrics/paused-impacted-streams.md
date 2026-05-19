---
title: 일시 중지된 영향을 받은 스트림
description: 뷰어가 일시 중지된 세션을 한 번 이상 카운트합니다.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 11%

---


# 일시 중지된 영향을 받은 스트림

**일시 중지된 영향을 받은 스트림** 지표는 뷰어가 일시 중지된 세션을 한 번 이상 계산합니다. 세션 수준 부울입니다. 하나의 영향을 받은 스트림과 동일한 세션 카운트 내에서 여러 번의 일시 중지가 발생합니다. 일시 중지가 발생한 세션의 공유를 측정하는 데 사용합니다. 총 일시 중지 볼륨의 경우 [일시 중지 이벤트](pause-events.md)를 사용합니다.

## 이 지표의 계산 방법

세션 중에 [일시 중지 시작](/help/implementation/events/playback/pause-start.md) 이벤트가 처음 수신되면 미디어 백엔드가 `mediaReporting.sessionDetails.hasPauseImpactedStreams = true`을(를) 설정합니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.pause`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasPauseImpactedStreams`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | 해당 사항 없음 |
