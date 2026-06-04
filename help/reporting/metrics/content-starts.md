---
title: 컨텐츠 시작
description: 기본 콘텐츠가 실제로 재생되기 시작한 세션을 카운트합니다.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 10%

---


# 컨텐츠 시작

**콘텐츠 시작** 지표는 기본 콘텐츠가 실제로 재생을 시작한 세션을 계산합니다. [미디어 시작](media-starts.md)과 달리, 프리롤 광고, 버퍼링 또는 중지 중에 종료된 세션은 제외됩니다. 이를 통해 완료 및 참여율에 적합한 분모가 됩니다.

## 이 지표의 계산 방법

미디어 백엔드는 기본 콘텐츠에 대한 [play](/help/implementation/events/playback/play.md) 이벤트가 처음 수신될 때 이 플래그를 설정합니다. 지표는 해당 재생 이벤트에서 트리거되지만 닫기 호출에 보고됩니다. 프리롤 드롭 속도를 계산하려면 `(Media starts − Content starts) / Media starts`을(를) 사용합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.play`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isPlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.play` |
