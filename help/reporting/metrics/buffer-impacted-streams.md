---
title: 버퍼의 영향을 받는 스트림
description: 플레이어가 버퍼 상태에 들어간 세션을 한 번 이상 카운트합니다.
feature: Metrics
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 10%

---


# 버퍼의 영향을 받는 스트림

**버퍼 영향을 받은 스트림** 지표는 플레이어가 버퍼 상태에 한 번 이상 들어간 세션을 계산합니다. 지표는 세션 수준 부울이며, 동일한 세션 카운트 내에 있는 여러 버퍼 이벤트가 하나의 영향을 받은 스트림과 같습니다. 총 버퍼 볼륨에 대해 [버퍼 이벤트](buffer-events.md)를 사용하십시오.

## 이 지표의 계산 방법

세션 중에 [버퍼 시작](/help/implementation/events/playback/buffer-start.md) 이벤트가 처음 수신되면 미디어 백엔드가 이 플래그를 설정합니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.buffer`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasBufferImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.qoe.buffer` |
