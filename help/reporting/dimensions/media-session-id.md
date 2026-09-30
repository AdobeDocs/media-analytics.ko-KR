---
title: 미디어 세션 ID
description: 각 재생 세션을 고유하게 식별합니다.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 6%
---

# 미디어 세션 ID

**미디어 세션 ID** 차원은 각 재생 세션을 고유하게 식별합니다. 백엔드에서 생성되고 세션에 대한 모든 이벤트에 스탬프가 지정됩니다. 이 플러그인을 사용하여 디버깅을 위해 단일 세션의 이벤트를 분리하거나 사용자 지정 분석에서 세션의 중복을 제거합니다.

## 이 차원이 채워지는 방법

백엔드가 [세션 시작](/help/implementation/events/session/session-start.md) 이벤트를 받으면 세션 ID가 자동으로 생성됩니다. 웹 SDK 및 Mobile SDK 구현은 ID를 캡처하고 유지합니다. 직접 API 구현은 `sessionStart` 응답(Media Collection API의 `Location` 헤더 또는 Media Edge API의 `media-analytics:new-session` 핸들)에서 세션 ID를 읽고 후속 이벤트에 포함해야 합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | `a.media.vsid`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videosessionid`, `post_videosessionid` |
| Audience Manager | `c_contextdata.a.media.vsid` |

## 차원 항목

각 항목은 백엔드에서 생성된 고유한 세션 ID입니다(일반적으로 22자 영숫자 문자열). 필터 또는 검색 필드를 사용하여 특정 세션을 조회합니다.
