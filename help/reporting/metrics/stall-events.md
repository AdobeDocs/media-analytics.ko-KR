---
title: 중지 이벤트
description: 세션 간 합계 및 평균에 대한 지연 이벤트를 계산합니다.
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
source-wordcount: '203'
ht-degree: 7%
---

# 중지 이벤트

**중지 이벤트** 지표는 합계, 평균 및 백분위수 롤업에 적합한 세션 간 중지 이벤트를 계산합니다. 지표를 사용하여 보고서 기간의 총 지연 볼륨을 계산하고 콘텐츠, 네트워크 또는 플레이어 간의 지연 안정성을 비교합니다.

Customer Journey Analytics에서 `xdm.mediaReporting.qoeDataDetails.stallCount`은(는) 별도의 차원 구성 요소 없이 지표 또는 차원으로 사용할 수 있습니다.

## 이 지표의 계산 방법

미디어 백엔드는 최소 3개의 연속 이벤트 동안 기본 콘텐츠에 플레이헤드 이동이 기록되지 않을 때마다 카운트를 증가시킵니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | `a.media.qoe.stallCount`을(를) 사용자 지정 이벤트에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/ko/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.stallCount`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`(처리 규칙이 `a.media.qoe.stallCount`을(를) 매핑하는 사용자 지정 이벤트. [`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.qoe.stallCount` |

세션 수준 부울 보고(지연이 전혀 발생하지 않았는지 여부)의 경우 [영향을 받은 스트림 중단](stall-impacted-streams.md)을 사용합니다.
