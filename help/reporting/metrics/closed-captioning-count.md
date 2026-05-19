---
title: 자막 카운트
description: 세션 중 뷰어가 캡션을 활성화한 횟수를 보고합니다.
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 8%

---


# 자막 카운트

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**자막 카운트**&#x200B;보고 지표를 다룹니다. 이 변수를 수집하는 방법은 [자막](/help/implementation/variables/player-state/closed-captioning.md)을 참조하세요.*

>[!ENDSHADEBOX]

**폐쇄 캡션 수** 지표는 세션 중 뷰어가 캡션을 사용하도록 설정한 횟수를 보고합니다. 각 캡션 활성화 상태 시작 이벤트는 개수를 증가시킵니다. 세션 수준 부울 롤업에 대해 [닫힌 캡션의 영향을 받은 스트림](closed-captioning-streams-impacted.md)과(와) 상태의 총 시간에 대해 [닫힌 캡션 총 기간](closed-captioning-total-duration.md)을 연결합니다.

## 이 지표의 계산 방법

미디어 백엔드는 모든 캡션 사용 상태 시작 이벤트에서 이 카운트를 증가시킵니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 플레이어 상태 추적]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.states.closedcaptioning.count`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/media-reporting-details) 항목 위치: `name = "closedCaptioning"`, 필드: `count` |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.count` |
