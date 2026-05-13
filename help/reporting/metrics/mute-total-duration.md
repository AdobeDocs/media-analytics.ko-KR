---
title: 음소거 총 기간
description: 세션 중에 오디오가 음소거된 누적 시간(초)을 보고합니다.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 7%

---


# 음소거 총 기간

>[!BEGINSHADEBOX]

*이 페이지는&#x200B;**음소거 총 기간**&#x200B;보고 지표에 적용됩니다. 이 변수를 수집하는 방법은 [음소거](/help/implementation/variables/player-state/mute.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**음소거 총 기간** 지표는 세션 중에 오디오가 음소거된 누적 시간(초)을 보고합니다. 백엔드는 음소거 상태 시작과 일치하는 상태 끝 이벤트 사이의 모든 간격을 합산합니다.

## 이 지표의 계산 방법

미디어 백엔드는 세션 중 모든 음소거 간격에 걸쳐 경과된 시간을 합산합니다. 지표는 닫기 호출에 보고됩니다. Analysis Workspace은 값을 `HH:MM:SS`(으)로 표시합니다. 데이터 피드, Data Warehouse 및 보고 API는 값(초)을 표시합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 플레이어 상태 추적]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.states.mute.time`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) 항목 위치: `name = "mute"`, 필드: `time` |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
