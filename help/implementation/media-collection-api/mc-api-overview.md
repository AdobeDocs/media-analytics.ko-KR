---
seo-title: Overview
title: 스트리밍 미디어 컬렉션 API 개요
description: Media Collection API에 대하여 알아보고 플레이어가 RESTful HTTP 호출을 사용하여 오디오 및 비디오를 추적하는 방법에 대해 알아봅니다.
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
exl-id: 58430636-7fab-433a-8ead-52ccaa45d920
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/79XLYzuvi3neUuCrt3LcGEwnnaR038-mWHMuSrY797M
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: 347
ht-degree: 91%

---

# Media Collection API 개요 {#overview}

Media Collection API는 고객 측 Media SDK에 대한 Adobe의 RESTful 대안입니다. Media Collection API를 사용하면 플레이어에서 RESTful HTTP 호출을 사용하여 오디오 및 비디오 이벤트를 추적할 수 있습니다.

Media Collection API는 본질적으로 Media SDK의 서버 측 버전 역할을 하는 어댑터입니다. 수집된 스트리밍 미디어 추적 데이터는 동일한 [보고 및 분석](/help/reporting/media-reports-enable.md)으로 이어집니다.

## 미디어 추적 데이터 흐름 {#media-tracking-data-flows}

Media Collection API를 구현하는 미디어 플레이어는 미디어 추적 백 엔드 서버에 직접 RESTful API 추적 호출을 수행하지만, Media SDK를 구현하는 플레이어는 플레이어 앱 내의 SDK API에 대한 추적 호출을 수행합니다. 웹을 통해 호출하면 Media Collection API를 구현하는 플레이어가 Media SDK에서 자동으로 처리하는 과정의 일부를 처리해야 합니다. ([Media Collection 구현](mc-api-impl/mc-api-quick-start.md)의 세부 사항)

Media Collection API로 캡처된 추적 데이터는 전송되고 Media SDK 플레이어에서 캡처된 추적 데이터와 처음에는 다르게 처리되지만, 백 엔드에서 동일한 처리 엔진이 두 솔루션에 모두 사용됩니다.

![](assets/col_api_overview_simple.png)

## API 개요 {#api-overview}

**URI:** Adobe 담당자에게서 얻습니다.

**HTTP 메서드:** JSON 요청 본문이 있는 POST

### API 호출 {#mc-api-calls}

* **`sessions`-** 서버의 세션을 설정하고, 후속 `events` 호출에 사용된 세션 ID를 반환합니다. 앱에서 추적 세션이 시작될 때 이 ID를 한 번 호출합니다.

  `{uri}/api/v1/sessions`

* **`events`-** 미디어 추적 데이터를 보냅니다.

  `{uri}/api/v1/sessions/{session-id}/events`

### 요청 본문 {#mc-api-request-body}

```json
{
    "playerTime": {
        "playhead": "{playhead position in seconds}",
        "ts": "{timestamp in milliseconds}"
    },
    "eventType": "{event-type}",
    "params": {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    },
    "qoeData" : {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    },
    "customMetadata": {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    }
}
```

* `playerTime` - 모든 요청에 필수입니다.
* `eventType` - 모든 요청에 필수입니다.
* `params` - 특정 `eventTypes`에 필수입니다. [JSON 유효성 검사 스키마](mc-api-ref/mc-api-json-validation.md)에서 필수 eventTypes과 옵션 eventTypes를 확인합니다.

* `qoeData` - 모든 요청에 선택 사항입니다.
* `customMetadata` - 모든 요청에 선택 사항이지만, `sessionStart`, `adStart` 및 `chapterStart` 이벤트 유형과 함께 전송됩니다.

각 `eventType`의 경우 매개 변수 유형을 확인하고 매개 변수가 특정 이벤트에 필수인지 또는 선택 사항인지 확인하는 데 사용해야 하는 [JSON 유효성 검사 스키마](mc-api-ref/mc-api-json-validation.md)가 있으며, 이 스키마는 공개적으로 제공됩니다.

### 이벤트 유형 {#mc-api-event-types}

SDK 단위 구현 예제를 사용하는 이벤트 유형의 전체 목록에 대해서는 [이벤트 개요](/help/implementation/events/overview.md)를 참조하십시오.
