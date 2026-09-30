---
title: 광고 완료
description: 완료까지 재생된 모든 광고를 카운트합니다.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 12%
---

# 광고 완료

**광고 완료** 지표는 완료 시까지 재생된 모든 광고를 계산합니다. 광고 완료율을 계산하려면 광고 시작을 [개](ad-starts.md)와(과) 연결하세요.

## 이 지표의 계산 방법

[광고 완료](/help/implementation/events/ads/ad-complete.md) 이벤트가 수신되면 미디어 백엔드가 이 플래그를 설정합니다. 지표는 광고 닫기 호출에 보고됩니다. 생략되거나 포기된 광고는 완료로 계산되지 않습니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 광고]](/help/reporting/setup/analytics-reporting.md)를 사용하도록 설정한 경우 컨텍스트 데이터 `a.media.ad.complete`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.isCompleted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.ad.complete` |
