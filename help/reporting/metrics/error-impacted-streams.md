---
title: 오류의 영향을 받은 스트림
description: 하나 이상의 오류가 발생한 세션을 카운트합니다.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 10%

---


# 오류의 영향을 받은 스트림

**오류 영향을 받은 스트림** 지표는 하나 이상의 오류가 발생한 세션을 계산합니다(`trackError`이 호출되었거나 [오류](/help/implementation/events/error.md) 이벤트가 실행됨). 이 지표는 세션 수준 부울입니다. 동일한 세션 내에서 여러 오류가 발생하면 영향을 받은 하나의 스트림과 계산됩니다. 총 오류 볼륨에 대해서는 [오류](/help/reporting/dimensions/errors.md)를 사용하십시오.

## 이 지표의 계산 방법

세션 중에 [오류](/help/implementation/events/error.md) 이벤트가 처음 수신되면 미디어 백엔드가 이 플래그를 설정합니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.error`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasErrorImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.qoe.error` |
