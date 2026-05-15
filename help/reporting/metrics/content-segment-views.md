---
title: 컨텐츠 세그먼트 보기 수
description: 활성 기본 컨텐츠 재생이 발생한 세그먼트를 계산합니다.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 9%

---


# 컨텐츠 세그먼트 보기 수

**콘텐츠 세그먼트 보기 수** 지표는 활성 기본 콘텐츠 재생이 발생한 5분 콘텐츠 세그먼트를 계산합니다. 지표는 시청자가 단순히 로드나 버퍼링이 아닌 해당 세그먼트에서 콘텐츠를 재생했음을 확인합니다. [콘텐츠 세그먼트](/help/reporting/dimensions/content-segment.md) 차원과 연결하여 긴 형식의 콘텐츠 뷰어에서 실제로 소비한 부분을 분류합니다.

## 이 지표의 계산 방법

미디어 백엔드는 기본 콘텐츠에 대한 하나 이상의 [play](/help/implementation/events/playback/play.md) 이벤트가 수신된 세그먼트를 포함하는 모든 닫기 호출에 대해 `mediaReporting.sessionDetails.hasSegmentView = true`을(를) 설정합니다. 지표는 닫기 호출에 보고됩니다. Media Edge API 경로에서 세그먼트 보기는 컨텐츠가 시작될 때와 동일한 조건에서 실행됩니다. 둘 다 기본 콘텐츠에 [play](/help/implementation/events/playback/play.md) 이벤트가 필요합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.segmentView`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasSegmentView`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | 해당 사항 없음 |
