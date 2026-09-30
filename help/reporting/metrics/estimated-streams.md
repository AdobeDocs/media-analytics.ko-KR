---
title: 예상 스트림
description: 세션당 오디오 또는 비디오 스트림 수와 비슷합니다.
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
source-wordcount: '190'
ht-degree: 10%
---

# 예상 스트림

**예상 스트림** 지표는 세션당 오디오 또는 비디오 스트림 수와 비슷하며 총 재생 30분마다 스트림 하나가 계산됩니다. 이는 콘텐츠 신디케이션 계약을 위한 것이며 각 30분 소비 블록이 별도의 &quot;스트림&quot;으로 계산되는 근사치에 도달합니다.

## 이 지표의 계산 방법

미디어 백엔드는 이 지표를 `FLOOR(totalTimePlayed / 1800) + 1`(으)로 계산합니다. 여기서 `totalTimePlayed`은(는) [미디어 체류 시간](media-time-spent.md)입니다(초). 지표는 닫기 호출에 보고됩니다.

| 미디어 체류 시간 | 예상 스트림 |
| --- | --- |
| 0-29분 | 1 |
| 30-59분 | 2 |
| 60-89분 | 3 |
| 90분 이상 | 4+ |

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | `a.media.estimatedStreams`을(를) 사용자 지정 이벤트에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.estimatedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`(처리 규칙이 `a.media.estimatedStreams`을(를) 매핑하는 사용자 지정 이벤트. [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.estimatedStreams` |
