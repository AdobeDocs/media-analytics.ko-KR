---
title: 드롭된 프레임의 영향을 받는 스트림
description: 하나 이상의 프레임이 드롭된 세션을 카운트합니다.
feature: Metrics
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 11%

---


# 드롭된 프레임의 영향을 받는 스트림

**드롭된 프레임 영향을 받은 스트림** 지표는 하나 이상의 프레임이 드롭된 세션을 계산합니다. 지표는 세션 수준 부울이며, 동일한 세션 내에서 여러 번의 드롭이 하나의 영향을 받은 스트림과 계산됩니다. 총 드롭 볼륨에 대해서는 [드롭된 프레임](dropped-frames.md)을 사용하십시오.

## 이 지표의 계산 방법

세션 종료 시 QoE 개체의 `droppedFrames` 값이 0보다 큰 경우 미디어 백엔드가 이 플래그를 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.droppedFrames`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrames` |
