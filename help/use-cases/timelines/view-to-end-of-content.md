---
title: 미디어 추적 타임라인에 대해 알아보기
description: 플레이헤드 타임라인과 해당 사용자의 작업을 자세히 알아보십시오. 각 작업과 그에 수반되는 요청에 대한 세부 사항을 알아보십시오.
uuid: 0ff591d3-fa99-4123-9e09-c4e71ea1060b
exl-id: 16b15e03-5581-471f-ab0c-077189dd32d6
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 99%

---

# 타임라인 1 - 콘텐츠 끝까지 보기{#timeline-view-to-end-of-content}

## VOD, 프리롤 광고, 일시 정지, 버퍼링, 콘텐츠 끝까지 보기

다음 다이어그램은 플레이헤드 타임라인과 사용자 작업의 해당 타임라인을 보여 줍니다. 각 작업 및 추가 요청에 대한 세부 사항은 아래에 나와 있습니다.

![API 콘텐츠](assets/va_api_content.png)

![API 작업](assets/va_api_actions.png)

## 작업 세부 사항

### 작업 1 - 세션 시작 {#Action-1}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 자동 재생 또는 재생 단추를 누르면 비디오가 로드되기 시작합니다. | 0 | 0 | `/api/v1/sessions` |

이 호출은 비디오를 _재생하도록 사용자에게 신호_&#x200B;를 보냅니다.

세션 내의 모든 후속 추적 호출을 식별하는 데 사용되는 클라이언트에 세션 ID( `{sid}` )가 반환됩니다. 플레이어 상태가 아직 “재생 중”이 아니라 “시작 중”입니다.

필수 세션 매개 변수는 요청 본문의 `params` 맵에 포함해야 합니다. 세션에 대한 자세한 내용은 미디어 컬렉션 API 설명서를 참조하십시오.

백엔드에서 이 호출은 Adobe Analytics 시작 호출을 생성합니다.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType":"sessionStart, params" {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR_TS_ ]",
        "analytics.reportSuite": "[ _YOUR_RSID_ ]",
        "analytics.visitorId": "[ _YOUR_VISITOR_ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR_MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### 작업 2 - Ping 타이머 시작 {#Action-2}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱 시작 ping 이벤트 타이머 | 0 | 0 | `/api/v1/sessions/{sid}/events` | |

앱의 Ping 타이머를 시작합니다. 그러면 첫 번째 Ping 이벤트는 프리롤 광고가 있는 경우 1초, 없는 경우에는 10초 실행됩니다.

### 작업 3 - 광고 브레이크 시작 {#Action-3}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 프리롤 광고 브레이크 시작 추적 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

광고는 광고 브레이크 내에서만 추적할 수 있습니다.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType":"adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0,
        "media.ad.podSecond": 0
    }
}
```

### 작업 4 - 광고 시작 {#Action-4}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 프리롤 광고 1 시작 추적 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

첫 번째 프리롤 광고 추적을 시작합니다(15초). 이 `adStart`에 사용자 지정 메타데이터를 포함합니다.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType":"adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "001",
        "media.ad.length": 15,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://example.com",
        "media.ad.placementId": "sample_placement"
    },
    "customMetadata": {
        "myCustomData1": "CustomData1",
        "myCustomData2": "CustomData2"
    }
}
```

**참고: AdBreakStart와 AdStart 이벤트 사이에는 추가 재생 이벤트가 없어야 합니다.**

### 작업 5 - 광고 Ping {#Action-5}

#### 작업 5.1 - 광고 Ping 1 {#Action-5-1}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 1 | 0 | `/api/v1/sessions/{sid}/events` |

광고 내에서 1초마다 백 엔드를 ping합니다.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

#### 작업 5.2 - 광고 Ping 2 {#Action-5-2}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 2 | 0 | `/api/v1/sessions/{sid}/events` |

광고 내에서 1초마다 백 엔드를 ping합니다.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

#### 작업 5.3 - 광고 Ping 3 {#Action-5-3}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 3 | 0 | `/api/v1/sessions/{sid}/events` |

광고 내에서 1초마다 백 엔드를 ping합니다.

>[!NOTE]
>
>타임라인의 후속 광고는 간결성을 위해 1초 동안의 일련의 Ping을
>&#x200B;>표시하지 않습니다...

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### 작업 6 - 광고 완료 {#Action-6}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 프리롤 광고 1 완료 추적 | 15 | 0 | `/api/v1/sessions/{sid}/events` |

첫 번째 프리롤 광고의 끝을 추적합니다.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### 작업 7 - 광고 시작 {#Action-7}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 프리롤 광고 2 시작 추적 | 15 | 0 | `/api/v1/sessions/{sid}/events` |

두 번째 프리롤 광고의 시작을 추적합니다(7초).

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 2",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "2",
        "media.ad.creativeId": "44",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://example.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### 작업 8 - 광고 Ping {#Action-8}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 20 | 0 | `/api/v1/sessions/{sid}/events` |

1초마다 백 엔드를 Ping합니다.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### 작업 9 - 광고 완료 {#Action-9}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 프리롤 광고 2 완료 추적 | 22 | 0 | `/api/v1/sessions/{sid}/events` |

두 번째 프리롤 광고의 끝을 추적합니다.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### 작업 10 - 광고 브레이크 완료 {#Action-10}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 프리롤 광고 브레이크 완료 추적 | 22 | 0 | `/api/v1/sessions/{sid}/events` |

광고 브레이크가 끝났습니다.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakComplete"
}
```

### 작업 11 - 콘텐츠 재생 {#Action-11}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 재생 이벤트 추적 | 22 | 0 | `/api/v1/sessions/{sid}/events` |

`adBreakComplete` 이벤트 다음에 `play` 이벤트를 사용하여 플레이어를 “재생 중” 상태에 둡니다.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "play"
}
```

### 작업 12 - Ping {#Action-12}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 30 | 8 | `/api/v1/sessions/{sid}/events` |

10초마다 백엔드를 ping합니다.

```json
{
    "playerTime": {
        "playhead": 8,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### 작업 13 - 버퍼 시작 {#Action-13}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 버퍼 시작 이벤트가 발생함 | 33 | 11 | `/api/v1/sessions/{sid}/events` |

플레이어의 “버퍼링” 상태 이동을 추적합니다.

```json
{
    "playerTime": {
        "playhead": 11,
        "ts": "<timestamp>"
    }, "eventType": "bufferStart"
}
```

### 작업 14 - 버퍼 끝 {#Action-14}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 버퍼링이 종료됨, 앱이 콘텐츠 재시작 추적 | 36 | 11 | `/api/v1/sessions/{sid}/events` |

버퍼링은 3초 후에 종료되므로 플레이어를 &quot;재생 중&quot; 상태로 되돌려 놓습니다. 버퍼링에서 나온 다른 추적 재생 이벤트를 보내야 합니다.  **`bufferStart` 다음에 `play`를 호출하면 &quot;버퍼엔드&quot;가 백 엔드를 호출한다고 유추하므로** `bufferEnd` 이벤트가 필요하지 않습니다.

```json
{
    "playerTime": {
        "playhead": 11,
        "ts": "<timestamp>"
    },
    "eventType": "play"
}
```

### 작업 15 - Ping {#Action-15}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 40 | 15 | `/api/v1/sessions/{sid}/events` |

10초마다 백엔드를 ping합니다.

```json
{
    "playerTime": {
        "playhead": 15,
        "ts": "<timestamp>"
    }, "eventType": "ping"
}
```

### 작업 16 - 광고 브레이크 시작 {#Action-16}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 미드롤 광고 브레이크 시작 추적 | 46 | 21 | `/api/v1/sessions/{sid}/events` |

8초 동안의 미드롤 광고: `adBreakStart`를 보냅니다.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 21
    }
}
```

### 작업 17 - 광고 시작 {#Action-17}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 미드롤 광고 3 시작 추적 | 46 | 21 | `/api/v1/sessions/{sid}/events` |

미드롤 광고를 추적합니다.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.name": "Ad 3",
        "media.ad.id": "003",
        "media.ad.length": 8,
        "media.ad.podPosition": 2,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "7",
        "media.ad.creativeId": "40",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://example.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### 작업 18 - 광고 Ping {#Action-18}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 50 | 21 | `/api/v1/sessions/{sid}/events` |

10초마다 백엔드를 ping합니다.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    }, "eventType": "ping"
}
```

### 작업 19 - 광고 완료 {#Action-19}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 미드롤 광고 1 완료 추적 | 54 | 21 | `/api/v1/sessions/{sid}/events` |

미드롤 광고가 완료되었습니다.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### 작업 20 - 광고 브레이크 완료 {#Action-20}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 미드롤 광고 브레이크 완료 추적 | 54 | 21 | `/api/v1/sessions/{sid}/events` |

광고 브레이크가 완료되었습니다.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakComplete"
}
```

### 작업 21 - Ping {#Action-21}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 60 | 27 | `/api/v1/sessions/{sid}/events` |

10초마다 백엔드를 ping합니다.

```json
{
    "playerTime": {
        "playhead": 27,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### 작업 22 - 일시 중지 {#Action-22}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 사용자가 일시 정지를 누름 | 64 | 31 | `/api/v1/sessions/{sid}/events` |

사용자의 작업이 재생 상태를 “일시 정지됨”으로 이동합니다.

```json
{
    "playerTime": {
        "playhead": 31,
        "ts": "<timestamp>"
    },
    "eventType": "pauseStart"
}
```

### 작업 23 - Ping {#Action-23}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 70 | 31 | `/api/v1/sessions/{sid}/events` |

10초마다 백엔드를 ping합니다. 플레이어가 여전히 &quot;버퍼링&quot; 상태입니다. 사용자가 콘텐츠에서 20초 후에 멈췄습니다. 계속...

```json
{
    "playerTime": {
        "playhead": 31,
        "ts": "<timestamp>"
    }, "eventType": "ping"
}
```

### 작업 24 - 재생 {#Action-24}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 사용자가 재생을 눌러 주 콘텐츠를 다시 시작함 | 74 | 31 | `/api/v1/sessions/{sid}/events` |

재생 상태를 &quot;재생 중&quot;으로 이동합니다.  **`pauseStart` 다음에 `play`를 호출하면 &quot;다시 시작&quot;이 백 엔드를 호출한다고 유추하므로,** `resume` 이벤트가 필요하지 않습니다.

```json
{
    "playerTime": {
        "playhead": 31,
        "ts": "<timestamp>"
    }, "eventType": "play"
}
```

### 작업 25 - Ping {#Action-25}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 80 | 37 | `/api/v1/sessions/{sid}/events` |

10초마다 백엔드를 ping합니다.

```json
{
    "playerTime": {
        "playhead": 37,
        "ts": "<timestamp>"
    }, "eventType": "ping"
}
```

### 작업 26 - 세션 완료 {#Action-26}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 사용자가 끝까지 콘텐츠 보기를 완료합니다. | 88 | 45 | `/api/v1/sessions/{sid}/events` |

`sessionComplete`를 백엔드에 보내어 사용자가 전체 콘텐츠 보기를 완료했음을 나타냅니다.

```json
{
    "playerTime": {
        "playhead": 45,
        "ts": "<timestamp>"
    }, "eventType": "sessionComplete"
}
```

>[!NOTE]
>
>**검색 이벤트가 없습니까?**- `seekStart` 또는 `seekComplete` 이벤트에 대한 Media Collection API에 명시적인 지원이 없습니다. 최종 사용자가 이동할 때 특정 플레이어에서 그러한 이벤트를 많이 생성하여 수백 명의 사용자가 백엔드 서비스의 네트워크 대역폭에 쉽게 병목 현상을 일으킬 수 있기 때문입니다. Adobe는 플레이헤드 위치가 아니라 디바이스 타임스탬프를 기반으로 하트비트 지속 시간을 계산하여 검색 이벤트에 대한 명시적 지원을 해결합니다.
