---
title: 비트율 변경의 영향을 받는 스트림
description: 하나 이상의 비트율 변경이 발생한 세션을 카운트합니다.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 9%

---


# 비트율 변경의 영향을 받는 스트림

**비트 전송률 변경은 스트림**&#x200B;에 영향을 주었습니다. 이 지표는 하나 이상의 비트 전송률 변경이 발생한 세션을 계산합니다. 지표는 세션 수준 부울입니다. 영향을 받은 하나의 스트림과 동일한 세션 카운트 내에서 여러 비트율 변경이 이루어집니다. 총 비트율 변경 볼륨에 대해서는 [비트율 변경](/help/reporting/dimensions/bitrate-changes.md)을 사용하십시오.

## 이 지표의 계산 방법

세션 중에 `media.bitrateChange` 이벤트가 처음 수신되면 미디어 백엔드가 `mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams = true`을(를) 설정합니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.bitrateChange`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
