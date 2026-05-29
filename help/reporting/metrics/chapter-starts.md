---
title: 챕터 시작
description: 세션 중에 재생되기 시작한 모든 챕터를 계산합니다.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 12%

---


# 챕터 시작

**챕터 시작** 지표는 세션 중에 재생되기 시작한 모든 챕터를 계산합니다. [챕터 완료](chapter-completes.md)와(과) 연결하여 챕터 완료율을 계산합니다.

## 이 지표의 계산 방법

[챕터 시작](/help/implementation/events/chapters/chapter-start.md) 이벤트가 수신되면 미디어 백엔드가 이 플래그를 설정합니다. 지표는 챕터 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 챕터]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.chapter.view`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.chapter.view` |
