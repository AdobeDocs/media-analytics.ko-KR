---
title: 영향을 받는 스트림 중단
description: 재생 도중 하나 이상의 지연이 발생한 세션을 카운트합니다.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 8%

---


# 영향을 받는 스트림 중단

**영향을 받는 스트림 중단** 지표는 재생 중에 하나 이상의 중단이 발생한 세션을 계산합니다. 지표는 세션 수준 부울입니다. 동일한 세션 내에 있는 여러 개의 정지가 하나의 영향을 받은 스트림과 계산됩니다. 총 중지 볼륨의 경우 [중지 이벤트](stall-events.md)를 사용하십시오.

## 이 지표의 계산 방법

세션 중에 최소 3개의 연속 이벤트 동안 기본 콘텐츠에 플레이헤드 이동이 기록되지 않으면 미디어 백엔드가 이 플래그를 설정합니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | `a.media.qoe.stall`을(를) 사용자 지정 이벤트에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/ko/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasStallImpactedStreams`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`(처리 규칙이 `a.media.qoe.stall`을(를) 매핑하는 사용자 지정 이벤트. [`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.qoe.stall` |
