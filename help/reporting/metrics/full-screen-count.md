---
title: 전체 화면 카운트
description: 세션 중 뷰어가 전체 화면으로 입력된 횟수를 보고합니다.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 7%

---


# 전체 화면 카운트

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**전체 화면 수**보고 지표를 다룹니다. 이 변수를 수집하는 방법은 [전체 화면](/help/implementation/variables/player-state/full-screen.md)을 참조하세요.*

>[!ENDSHADEBOX]

**전체 화면 수** 지표는 세션 중에 뷰어가 전체 화면을 입력한 횟수를 보고합니다. 각 전체 화면 상태 시작 이벤트는 카운트를 증가시킵니다. 세션 수준 부울 롤업에 대한 [전체 화면의 영향을 받은 스트림](full-screen-streams-impacted.md) 및 상태에 있는 총 시간에 대한 [전체 화면 총 기간](full-screen-total-duration.md)과 결합합니다.

## 이 지표의 계산 방법

미디어 백엔드는 모든 전체 화면 상태 시작 이벤트에서 `mediaReporting.states[]`의 `fullscreen` 항목에 있는 `count` 필드를 증가시킵니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 플레이어 상태 추적]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.states.fullscreen.count`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) 항목 위치: `name = "fullscreen"`, 필드: `count` |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
