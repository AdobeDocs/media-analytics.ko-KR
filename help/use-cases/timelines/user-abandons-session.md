---
title: 미디어 추적 타임라인 - 사용자가 세션을 중단함에 대해 알아보기
description: 비디오 세션이 중단될 때 플레이헤드 타임라인 및 해당 사용자의 작업에 대해 알아봅니다. 각 작업과 요청에 대한 세부 사항에 대해 알아봅니다.
uuid: 74b89e8f-ef56-4e0c-b9a8-40739e15b4cf
exl-id: 0c6a89f4-7949-4623-8ed9-ce1d1547bdfa
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4c68f5997a9d336e8c3545cdfb7b9cb955602b69
workflow-type: ht
source-wordcount: '600'
ht-degree: 100%

---

# 타임라인 2 - 사용자가 세션을 중단함 {#timeline--2-user-abandons-session}

## VOD, 프리롤 광고, 미드롤 광고, 사용자가 일찍 콘텐츠를 중단함

다음 다이어그램은 플레이헤드 타임라인과 사용자 작업의 해당 타임라인을 보여 줍니다. 각 작업 및 추가 요청에 대한 세부 사항은 아래에 나와 있습니다.

![API 콘텐츠](assets/va_api_content_2.png)

![API 작업](assets/va_api_actions_2.png)

## 작업 세부 사항

### 작업 1 - 세션 시작 {#Action-1}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 자동 재생 또는 재생 버튼 누름 | 0 | 0 | `/api/v1/sessions` |

이 호출은 비디오를 _재생하도록 사용자에게 신호_&#x200B;를 보냅니다. 세션 내의 모든 후속 추적 호출을 식별하는 데 사용되는 클라이언트에 세션 ID( `{sid}` )가 반환됩니다. 플레이어 상태가 아직 &quot;재생 중&quot;이 아니라 &quot;시작 중&quot;입니다.  필수 세션 매개 변수는 요청 본문의 `params` 맵에 포함해야 합니다.  백엔드에서 이 호출은 Adobe Analytics 시작 호출을 생성합니다. 세션에 대한 자세한 내용은 미디어 컬렉션 API 설명서를 참조하십시오.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "sessionStart",
    "params": {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR-TS_ ]",
        "analytics.reportSuite": "[ _YOUR-RSID_ ]",
        "analytics.visitorId": "[ _YOUR-VISITOR-ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR-MCID]",
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
| 앱 시작 ping 이벤트 타이머 | 0 | 0 |  |

앱의 Ping 타이머를 시작합니다. 그러면 첫 번째 Ping 이벤트는 프리롤 광고가 있는 경우 1초, 없는 경우에는 10초 실행됩니다.

### 작업 3 - 광고 브레이크 시작 {#Action-3}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 프리롤 광고 브레이크 시작 추적 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

프리롤 광고를 추적해야 합니다. 광고는 광고 브레이크 내에서만 추적할 수 있습니다.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakStart",
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

12초 광고가 시작됩니다.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz-creative.com",
        "media.ad.placementId": "sample-placement2"
    },
}
```

### 작업 5 - 광고 Ping {#Action-5}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 1 | 0 | `/api/v1/sessions/{sid}/events` |

1초마다 백 엔드를 Ping합니다. (간결성을 위해 후속 광고 Ping은 표시되지 않습니다.)

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
| 프리롤 광고 1 완료 추적 | 12 | 0 | `/api/v1/sessions/{sid}/events` |

첫 번째 프리롤 광고가 끝났습니다.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### 작업 7 - 광고 브레이크 완료 {#Action-7}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 프리롤 광고 브레이크 완료 추적 | 12 | 0 | `/api/v1/sessions/{sid}/events` |

광고 브레이크가 끝났습니다. 광고 브레이크 기간 동안 플레이어가 &quot;재생&quot; 상태로 남았습니다.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakComplete"
}
```

### 작업 8 - 콘텐츠 재생 {#Action-8}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 재생 이벤트 추적 | 12 | 0 | `/api/v1/sessions/{sid}/events` |

플레이어를 “재생 중” 상태로 이동하고, 콘텐츠 재생 시작을 추적하기 시작합니다.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "play",
    "qoeData": {
        "bitrate": 10000
    }
}
```

### 작업 9 - Ping {#Action-9}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 20 | 8 | `/api/v1/sessions/{sid}/events` |

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

### 작업 10 - Ping {#Action-10}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 30 | 18 | `/api/v1/sessions/{sid}/events` |

10초마다 백엔드를 ping합니다.

```json
{
    "playerTime": {
        "playhead": 18,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### 작업 11 - 오류 {#Action-11}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 오류가 발생하여 앱에서 오류 정보를 보냅니다. | 32 | 20 | `/api/v1/sessions/{sid}/events` |

```json
{
    "playerTime": {
        "playhead": 20,
        "ts": "<timestamp>"
    },
    "eventType": "error"
}
```

### 작업 12 - 콘텐츠 재생 {#Action-12}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱이 오류에서 복구되어 사용자가 재생을 누름 | 37 | 20 | `/api/v1/sessions/{sid}/events` |

```json
{
    "playerTime": {
        "playhead": 18,
        "ts": "<timestamp>"
    },
    "eventType":"play",
    "qoeData": {
        "bitrate": 10000
    }
}
```

### 작업 13 - Ping {#Action-13}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 앱에서 ping 이벤트 보내기 | 40 | 28 | `/api/v1/sessions/{sid}/events` |

10초마다 백엔드를 ping합니다.

```json
{
    "playerTime": {
        "playhead": 28,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### 작업 14 - 광고 브레이크 시작 {#Action-14}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 미드롤 광고 브레이크 시작 추적 | 45 | 33 | `/api/v1/sessions/{sid}/events` |

8초 동안의 미드롤 광고: `adBreakStart`를 보냅니다.

```json
{
    "playerTime": {
        "playhead": 33,
        "ts": "<timestamp>"
    },
    "eventType":"adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 33
    }
}
```

### 작업 15 - 광고 시작 {#Action-15}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 미드롤 광고 1 시작 추적 | 45 | 33 | `/api/v1/sessions/{sid}/events` |

미드롤 광고를 추적합니다.

```json
{
    "playerTime": { "playhead": 33, "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 8,
        "media.ad.podPosition": 1,
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

### 작업 16 - 앱 닫기 {#Action-16}

| 작업 | 작업 타임라인(초) | 플레이헤드 위치(초) | 클라이언트 요청 |
| --- | :---: | :---: | --- |
| 사용자가 앱을 닫습니다. 앱이 사용자가 보기를 중단하고 이 세션으로 돌아가지 않고 있다고 판단합니다. | 48 | 33 | `/api/v1/sessions/{sid}/events` |

`sessionEnd`를 VA 백엔드에 보내어 추가 처리 없이 세션을 즉시 닫아야 한다는 것을 나타냅니다.

```json
{
    "playerTime": {
        "playhead": 33,
        "ts": "<timestamp>"
    },
    "eventType": "sessionEnd"
}
```
