---
title: 총 중단 기간
description: 세션 간 합계와 평균에 대한 누적 중단 시간을 보고합니다.
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
source-wordcount: '210'
ht-degree: 7%
---

# 총 중단 기간

**총 중단 기간** 지표는 합계, 평균 및 백분위수 롤업에 적합한 세션 간 누적 중단 시간을 보고합니다. 지표를 사용하여 뷰어가 보고서 기간에 정지된 재생을 기다리는 데 걸린 총 시간을 계산합니다.

Customer Journey Analytics에서 `xdm.mediaReporting.qoeDataDetails.stallTime`은(는) 별도의 차원 구성 요소 없이 지표 또는 차원으로 사용할 수 있습니다.

## 이 지표의 계산 방법

미디어 백엔드는 최소 3개의 연속 이벤트 동안 기본 콘텐츠에 플레이헤드 이동이 기록되지 않은 경우 감지된 각 중단 간격의 지속 시간을 합산합니다. 지표는 닫기 호출에 보고됩니다. Analysis Workspace은 값을 `HH:MM:SS`(으)로 표시합니다. 데이터 피드, Data Warehouse 및 보고 API는 값(초)을 표시합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | `a.media.qoe.stallTime`을(를) 사용자 지정 이벤트에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.stallTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`(처리 규칙이 `a.media.qoe.stallTime`을(를) 매핑하는 사용자 지정 이벤트. [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.qoe.stallTime` |
