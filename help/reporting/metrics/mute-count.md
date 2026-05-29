---
title: 음소거 카운트
description: 세션 중 뷰어가 오디오를 음소거한 횟수를 보고합니다.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 9%

---


# 음소거 카운트

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**음소거 카운트**보고 지표를 다룹니다. 이 변수를 수집하는 방법은 [음소거](/help/implementation/variables/player-state/mute.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**음소거 카운트** 지표는 세션 중 뷰어가 오디오를 음소거한 횟수를 보고합니다. 각 음소거 상태 시작 이벤트는 카운트를 증가시킵니다. 세션 수준 부울 롤업에 대한 [음소거의 영향을 받은 스트림](mute-streams-impacted.md)과(와) 상태의 총 시간에 대한 [음소거 총 기간](mute-total-duration.md)을(를) 연결합니다.

## 이 지표의 계산 방법

미디어 백엔드는 모든 음소거 상태 시작 이벤트에 대해 이 카운트를 증가시킵니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 플레이어 상태 추적]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.states.mute.count`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) 항목 위치: `name = "mute"`, 필드: `count` |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.states.mute.count` |
