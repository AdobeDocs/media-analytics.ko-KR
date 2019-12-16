---
title: 타임라인 3 - 챕터
description: null
uuid: 41b52072-e1cd-4dda-9253-31f3408924f6
translation-type: tm+mt
source-git-commit: 22f7c21feb55f54c0c92db17eadc509966715cf3

---


# 타임라인 3 - 챕터 {#timeline-3-chapters}

## VOD, 프리롤 광고, 일시 정지, 버퍼링, 컨텐츠 끝까지 보기


다음 다이어그램은 플레이헤드 타임라인과 사용자 작업의 해당 타임라인을 보여 줍니다. 각 작업 및 추가 요청에 대한 세부 사항은 아래에 나와 있습니다.


![](assets/va_api_content_3.png)


![](assets/va_api_actions_3.png)


## 작업 세부 사항


### 작업 1 - 세션 시작 {#Action-1}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 자동 재생 또는 재생 단추 누름, video starts loading. | 0 | 0 | `/api/v1/sessions` |

**구현 세부 사항**

이 호출은 비디오를 _재생하도록 사용자에게 신호_&#x200B;를 보냅니다. 세션 내의 모든 후속 추적 호출을 식별하는 데 사용되는 클라이언트에 세션 ID( `{sid}` )가 반환됩니다. 플레이어 상태가 아직 "재생 중"이 아니라 "시작 중"입니다. [필수 세션 매개 변수](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)는 요청 본문의 `params` 맵에 포함해야 합니다.  백엔드에서 이 호출은 Adobe Analytics 시작 호출을 생성합니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:sessionStart, params: {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR-TS_ ]",
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
| 앱이 ping 이벤트 타이머 시작 | 0 | 0 |  |

**구현 세부 사항**

Ping 타이머를 시작합니다. 그러면 첫 번째 Ping 이벤트는 프리롤 광고가 있는 경우 1초, 없는 경우에는 10초 실행됩니다.

### 작업 3 - 광고 브레이크 시작 {#Action-3}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 프리롤 광고 브레이크 추적 시작 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

광고는 광고 브레이크 내에서만 추적할 수 있습니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0, "media.ad.podSecond": 0
    }
}
```

### 작업 4 - 광고 시작 {#Action-4}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 프리롤 광고 1 시작 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

첫 번째 프리롤 광고 추적을 시작합니다(15초). 이 `adStart`에 사용자 지정 메타데이터를 포함합니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
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
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement"
    },
    customMetadata: {
        "myCustomData1": "CustomData1",
        "myCustomData2": "CustomData2"
    }
}
```

### 작업 5 - 광고 Ping {#Action-5}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 10 | 0 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

1초마다 백 엔드를 Ping합니다. (간결성을 위해 후속 광고 Ping은 표시되지 않습니다.)

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 작업 6 - 광고 완료 {#Action-6}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 프리롤 광고 1 추적 완료 | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

첫 번째 프리롤 광고의 끝을 추적합니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### 작업 7 - 광고 시작 {#Action-7}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 프리롤 광고 2 추적 시작 | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

두 번째 프리롤 광고의 시작을 추적합니다(7초).

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
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
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### 작업 8 - 광고 Ping {#Action-8}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 16 | 0 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

1초마다 백 엔드를 Ping합니다. (간결성을 위해 후속 광고 Ping은 표시되지 않습니다.)

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 작업 9 - 광고 완료 {#Action-9}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 프리롤 광고 2 추적 완료 | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

두 번째 프리롤 광고의 끝을 추적합니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### 작업 10 - 광고 브레이크 완료 {#Action-10}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 프리롤 광고 브레이크 추적 완료 | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

광고 브레이크가 끝났습니다. 광고 브레이크 전 기간 동안 재생 상태가 "재생 중"으로 남아 있습니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### 작업 11 - 컨텐츠 재생 {#Action-11}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 재생 이벤트 추적 | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

`adBreakComplete` 이벤트 다음에 `play` 이벤트를 사용하여 플레이어를 "재생 중" 상태에 둡니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play
}
```

### 작업 12 - 챕터 시작 {#Action-12}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 챕터 시작 이벤트 추적 | 23 | 1 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

재생 이벤트가 끝나면 첫 번째 챕터의 시작을 추적합니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:chapterStart, params: {
        "media.chapter.index": 1,
        "media.chapter.offset": 0, "media.chapter.length": 20, "media.chapter.friendlyName": "Chapter Uno"
    },
}
```

### 작업 13 - Ping {#Action-13}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 30 | 8 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

10초마다 백엔드를 ping합니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 8,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 작업 14 - 버퍼 시작 {#Action-14}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 버퍼 시작 이벤트 발생 | 33 | 11 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

버퍼링 상태 이동을 추적합니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:bufferStart
}
```

### 작업 15 - 버퍼 끝(재생) {#Action-15}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 버퍼링이 종료되면 앱이 컨텐츠 재개를 추적합니다. | 36 | 11 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

버퍼링은 3초 후에 종료되므로 플레이어를 "재생 중" 상태로 되돌려 놓습니다. 버퍼링에서 나온 다른 추적 재생 이벤트를 보내야 합니다.  **`bufferStart`다음에`play`를 호출하면 "버퍼엔드"가 백 엔드를 호출한다고 유추하므로** `bufferEnd` 이벤트가 필요하지 않습니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:play
}
```

### 작업 16 - Ping {#Action-16}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 40 | 15 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

10초마다 백엔드를 ping합니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 15,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 작업 17 - 챕터 종료 {#Action-17}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 챕터 끝 추적 | 45 | 20 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

첫 번째 챕터는 두 번째 광고 브레이크 직전에 종료됩니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 20,
        ts: <timestamp>
    },
    eventType:chapterComplete
}
```

### 작업 18 - 광고 브레이크 시작 {#Action-18}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 미드롤 광고 브레이크 추적 시작 | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

8초 동안의 미드롤 광고: `adBreakStart`를 보냅니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1, "media.ad.podSecond": 21
    }
}
```

### 작업 19 - 광고 시작 {#Action-19}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 미드롤 광고 3 추적 시작 | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

미드롤 광고를 추적합니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adStart, params: {
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
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### 작업 20 - 광고 Ping {#Action-20}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 47 | 21 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

1초마다 백 엔드를 Ping합니다. (간결성을 위해 후속 광고 Ping은 표시되지 않습니다.)

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 작업 21 - 광고 완료 {#Action-21}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 미드롤 광고 1 추적 완료 | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

미드롤 광고가 완료되었습니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### 작업 22 - 광고 브레이크 완료 {#Action-22}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 미드롤 광고 브레이크 추적 완료 | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

광고 브레이크가 완료되었습니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### 작업 23 - 챕터 시작 {#Action-23}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 챕터 2의 시작 추적 | 55 | 22 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**



**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 22,
        ts: <timestamp>
    },
    eventType:chapterStart, params: {
        "media.chapter.index": 2,
        "media.chapter.offset": 22, "media.chapter.length": 22, "media.chapter.friendlyName": "Chapter Dos"
    },
}
```

### 작업 24 - Ping {#Action-24}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 60 | 27 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

10초마다 백엔드를 ping합니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 27,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 작업 25 - 일시 중지 {#Action-25}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 사용자가 일시 정지를 누름 | 64 | 31 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

사용자의 작업이 재생 상태를 "일시 중지됨"으로 이동합니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:pauseStart
}
```

### 작업 26 - Ping {#Action-26}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 70 | 31 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

10초마다 백엔드를 ping합니다. 플레이어가 여전히 "버퍼링" 상태이므로, 사용자 작업이 20초 동안 중단됩니다. 퍼밍...

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 작업 27 - 컨텐츠 재생 {#Action-27}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 사용자가 재생을 눌러 기본 컨텐츠를 재개함 | 74 | 31 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

재생 상태를 "재생 중"으로 이동합니다.  **`play`다음에`pauseStart`를 호출하면 "resume"이 백 엔드를 호출한다고 유추하므로** `resume` 이벤트가 필요하지 않습니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:play
}
```

### 작업 28 - Ping {#Action-28}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 80 | 37 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

10초마다 백엔드를 ping합니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 37,
        ts: <timestamp>
    },
    eventType:ping
}
```

### 작업 29 - 챕터 종료 {#Action-29}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 챕터 2가 종료됨 | 87 | 44 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

두 번째 및 마지막 챕터의 끝을 추적합니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:chapterComplete
}
```

### 작업 30 - 세션 완료 {#Action-30}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 사용자가 컨텐츠 보기를 끝까지 완료합니다. | 88 | 45 | `/api/v1/sessions/{sid}/events` |

**구현 세부 사항**

`sessionComplete`를 백엔드에 보내어 사용자가 전체 컨텐츠 보기를 완료했음을 나타냅니다.

**샘플 요청 본문**

```
{
    playerTime: {
        playhead: 45,
        ts: <timestamp>
    },
    eventType:sessionComplete
}
```


>[!NOTE]
>
>**검색 이벤트가 없습니까?**- `seekStart` 또는 `seekComplete` 이벤트에 대한 Media Collection API에 명시적인 지원이 없습니다. 최종 사용자가 스크럽할 때 특정 플레이어가 그러한 수많은 이벤트를 생성하므로 수많은 사용자가 백엔드 서비스의 네트워크 대역폭을 쉽게 병목 현상이 발생하기 때문입니다. Adobe는 플레이헤드 위치가 아닌 장치 타임스탬프를 기반으로 한 하트비트 기간을 계산하여 찾기 이벤트에 대한 명시적인 지원을 제공합니다.

