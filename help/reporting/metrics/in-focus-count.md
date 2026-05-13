---
title: 초점 카운트
description: 세션 중 플레이어가 포커스를 얻은 횟수를 보고합니다.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 7%

---


# 초점 카운트

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**포커스 카운트**&#x200B;보고 지표를 다룹니다. 이 변수를 수집하는 방법은 [초점](/help/implementation/variables/player-state/in-focus.md)을 참조하세요.*

>[!ENDSHADEBOX]

**포커스 카운트** 지표는 세션 중에 플레이어가 포커스를 얻은 횟수를 보고합니다. 각 포커스 상태 시작 이벤트는 카운트를 증가시킵니다. 세션 수준 부울 롤업의 경우 [초점의 영향을 받은 스트림](in-focus-streams-impacted.md)과(와) 상태 총 시간의 경우 [초점 총 기간](in-focus-total-duration.md)을 연결합니다.

## 이 지표의 계산 방법

미디어 백엔드는 모든 포커스 상태 시작 이벤트에서 `mediaReporting.states[]`의 `inFocus` 항목에 있는 `count` 필드를 증가시킵니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 플레이어 상태 추적]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.states.infocus.count`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/media-reporting-details) 항목 위치: `name = "inFocus"`, 필드: `count` |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
