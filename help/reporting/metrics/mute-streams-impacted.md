---
title: 음소거의 영향을 받는 스트림
description: 뷰어가 오디오를 음소거한 세션을 한 번 이상 카운트합니다.
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 8%

---


# 음소거의 영향을 받는 스트림

>[!BEGINSHADEBOX]

*이 페이지에서는 음소거의 영향을 받는&#x200B;**스트림**보고 지표를 다룹니다. 이 변수를 수집하는 방법은 [음소거](/help/implementation/variables/player-state/mute.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**음소거의 영향을 받은 스트림** 지표는 뷰어가 오디오를 음소거한 세션을 한 번 이상 계산합니다. 지표는 세션 수준 부울입니다. 하나의 영향을 받은 스트림과 동일한 세션 카운트 내에서 여러 개의 음소거 전환이 가능합니다. 총 음소거 볼륨은 [음소거 카운트](mute-count.md)를 사용합니다.

## 이 지표의 계산 방법

미디어 백엔드는 세션 중에 음소거 상태 시작 이벤트가 처음 수신될 때 이 플래그를 설정합니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 플레이어 상태 추적]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.states.mute.set`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) 항목 위치: `name = "mute"`, 필드: `isSet` |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.states.mute.set` |
