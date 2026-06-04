---
title: 사용자 정의 메타데이터 지원
description: sessionStart, chapterStart 및 adStart 이벤트에서 사용자 지정 key:value 쌍을 제공하는 방법에 대해 알아봅니다.
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/sEVJa-FPqZiSc4Hdr7lQfNbECS2lxckBmqAYhGHmx2w
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 449
ht-degree: 7%

---

# 사용자 지정 메타데이터 지원{#custom-metadata-support}

Media Collection API를 사용하면 `sessionStart`, `adStart` 및 `chapterStart` 이벤트의 표준 매개 변수와 함께 사용자 지정 키-값 쌍을 보낼 수 있습니다. 사용자 지정 메타데이터는 각 미디어 닫기 이벤트를 사용하여 **Adobe Analytics**(으)로 전달됩니다.

이 데이터를 Analysis Workspace에서 사용할 수 있도록 하려면 고객은 사용자 지정 eVar를 정의하고 처리 규칙을 구성하여 사용 사례에 따라 채워야 합니다. eVar 또는 prop에 매핑되면 [Analytics 소스 커넥터](https://experienceleague.adobe.com/ko/docs/experience-platform/sources/connectors/adobe-applications/analytics)가 구성된 경우 해당 eVar 경로를 통해 Adobe Experience Platform에서도 데이터를 사용할 수 있게 됩니다.

Experience Edge을 사용하는 XDM 기반 구현의 경우 [사용자 지정 메타데이터 지원 - XDM 형식](/help/implementation/edge/custom-metadata.md)을 참조하십시오.

## 개요

사용자 지정 메타데이터는 `params` 키와 함께 배치된 `customMetadata` 개체로 요청 본문에 포함됩니다. 다음 세 가지 이벤트 유형에 적용됩니다.

| 이벤트 | 메타데이터 적용 대상 |
|-------|-------------------|
| `sessionStart` | 기본 컨텐츠(전체 세션) |
| `adStart` | 개별 광고 |
| `chapterStart` | 컨텐츠 챕터 또는 세그먼트 |

## 구조

사용자 지정 메타데이터는 이벤트 수준에서 `params` 키와 함께 플랫 **object**(키-값 쌍)입니다.

```json
{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "field": "value"
  }
}
```

### 이벤트 유형별 필수 매개 변수

| 이벤트 | 필수 `params` |
|-------|-------------------|
| `sessionStart` | `analytics.trackingServer`, `analytics.reportSuite`, `visitor.marketingCloudOrgId`, `media.id`, `media.length`, `media.contentType`, `media.playerName`, `media.channel` |
| `adStart` | `media.ad.id`, `media.ad.length`, `media.ad.podPosition`, `media.ad.playerName` |
| `chapterStart` | `media.chapter.length`, `media.chapter.offset`, `media.chapter.index` |

### 주요 이름 지정 요구 사항

* 사용자 지정 메타데이터 키에 `media.` 접두사를 사용하지 마십시오. 표준 미디어 필드에 매핑되면 Analytics 보고에서 덮어쓸 수 있습니다
* `a.` 접두사는 Adobe 표준 메타데이터용으로 예약되어 있으므로 사용할 수 없습니다.

## 기본 컨텐츠 사용자 지정 메타데이터

`sessionStart`(으)로 전송되었습니다. 추적 중인 기본 미디어에 적용되며 광고 및 챕터 호출 전체에서 사용할 수 있습니다. 여기에 정의된 모든 사용자 지정 메타데이터는 해당 닫기 호출 시 미디어 백엔드에 의해 자동으로 병합됩니다. 광고 및 챕터에 대해 정의된 특정 사용자 지정 메타데이터와 함께 포함됩니다.

```sh
curl -X POST "https://{uri}/api/v1/sessions" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "analytics.visitorId": "visitor123",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.name": "Sample Video",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "contentCategory": "Live Sports",
    "leagueType": "Professional",
    "broadcastRights": "Premium"
  }
}'
```

## 사용자 지정 메타데이터 추가

`adStart`(으)로 전송되었습니다. 각 개별 광고에만 해당됩니다. `sessionStart`의 사용자 지정 메타데이터도 여기에 정의된 광고 관련 사용자 지정 메타데이터와 함께 광고 닫기 호출에서 미디어 백엔드에 의해 자동으로 병합됩니다.

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 30,
    "ts": 1646938830000
  },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "summer-sale-2026",
    "media.ad.name": "Summer Sale Ad",
    "media.ad.length": 30,
    "media.ad.playerName": "HTML5 Player",
    "media.ad.podPosition": 1
  },
  "customMetadata": {
    "campaignId": "SUMMER2026",
    "targetAudience": "18-34",
    "adFormat": "skippable"
  }
}'
```

## 챕터 사용자 지정 메타데이터

`chapterStart`(으)로 전송되었습니다. 각 콘텐츠 챕터 또는 세그먼트에 대한 것입니다. `sessionStart`의 사용자 지정 메타데이터도 여기에 정의된 챕터별 사용자 지정 메타데이터와 함께 챕터 닫기 호출에서 미디어 백엔드에 의해 자동으로 병합됩니다.

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 600,
    "ts": 1646938200000
  },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Introduction",
    "media.chapter.length": 300,
    "media.chapter.index": 1,
    "media.chapter.offset": 600
  },
  "customMetadata": {
    "chapterType": "tutorial",
    "difficulty": "beginner",
    "instructor": "Jane Smith"
  }
}'
```

## 비헤이비어

* 모든 사용자 지정 메타데이터 값은 **문자열**&#x200B;이어야 합니다. 보내기 전에 숫자와 부울을 변환합니다.
* 사용자 지정 메타데이터가 Analytics에 `c.` 접두사로 나타납니다(예: `contentCategory` → `c.contentCategory`).
* Analytics 처리 규칙을 통해 사용자 지정 메타데이터를 eVar, prop 또는 컨텍스트 데이터 변수에 매핑
* `sessionStart` 메타데이터는 전체 세션 동안 지속되며 업데이트에는 새 세션이 필요합니다.
* 각 `adStart` 및 `chapterStart` 이벤트는 서로 다른 사용자 지정 메타데이터를 전달할 수 있습니다.

## 관련 설명서

* [사용자 지정 메타데이터 지원 - XDM 형식](/help/implementation/edge/custom-metadata.md) - 사용자 지정 메타데이터를 Experience Edge을 통해 Analytics와 AEP 모두에 보냅니다.
* [보고서 세트 데이터용 Adobe Analytics 소스 커넥터](https://experienceleague.adobe.com/ko/docs/experience-platform/sources/connectors/adobe-applications/analytics) - Analytics 데이터를 Adobe Experience Platform으로 가져오기

<!--
* [Session endpoints](sessions.md) — Session lifecycle management
* [Ad endpoints](ads.md) — Track advertising impressions
* [Chapter endpoints](chapters.md) — Segment content into chapters
-->
