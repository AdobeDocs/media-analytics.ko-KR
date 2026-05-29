---
title: 인증됨
description: Adobe Pass을 통해 사용자가 승인된 세션을 카운트합니다.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 12%

---


# 인증됨

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**인증됨**보고 지표를 다룹니다. 이 변수를 수집하는 방법은 [인증됨](/help/implementation/variables/standard-metadata/authorized.md)을 참조하십시오.*

>[!ENDSHADEBOX]

**인증됨** 지표는 사용자가 Adobe Pass 또는 TV-Everywhere를 통해 승인된 세션을 계산합니다. [MVPD](/help/reporting/dimensions/mvpd.md) 차원과 연결하여 공급자별로 인증 볼륨을 분류합니다.

## 이 지표의 계산 방법

미디어 백엔드는 플레이어가 세션 시작 시 승인된 세션으로 플래그를 지정할 때 카운트를 증가시킵니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 비디오 메타데이터]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.pass.auth`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.authorized`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.pass.auth` |
