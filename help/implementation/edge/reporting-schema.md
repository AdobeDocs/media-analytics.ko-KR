---
title: XDM 보고 스키마
description: Adobe Experience Platform에서 경험 이벤트를 생성하는 Media Edge API 이벤트와 mediaReporting XDM 스키마를 사용하여 구현의 유효성을 검사하는 방법을 알아봅니다.
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3a4d31b-8f9e-4d7a-9b2e-1a5f0e8c7d39
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 763
ht-degree: 4%

---


# XDM 보고 스키마

Adobe Experience Platform Edge Network을 사용하여 미디어 추적 이벤트를 전송하면 Media Analytics 백엔드가 해당 이벤트를 처리하고 계산된 Experience 이벤트를 Platform 데이터 세트에 기록합니다. Platform에 도달하는 이벤트와 백엔드가 자동으로 계산하는 내용을 이해하면 구현을 검증하고 Customer Journey Analytics 또는 Adobe Analytics에서 정확한 보고서를 작성하는 데 도움이 됩니다.

컬렉션 및 보고 파이프라인의 다른 부분에서 두 개의 고유한 XDM 스키마가 사용됩니다.

| 스키마 | 네임스페이스 | 방향 | 용도 |
|---|---|---|---|
| 미디어 컬렉션 | `xdm.mediaCollection` | 클라이언트 → Adobe | 플레이어가 각 추적 이벤트에 대해 보내는 내용입니다. [변수](/help/implementation/variables/)에서 사용됩니다. |
| 미디어 보고 | `xdm.mediaReporting` | Adobe → 플랫폼 | 처리 후 백엔드가 데이터 세트에 쓰는 내용. [차원](/help/reporting/dimensions/overview.md) 및 [지표](/help/reporting/metrics/overview.md)에서 사용됩니다. |

`mediaReporting`에 있지만 `mediaCollection` 페이로드에는 없는 필드는 세션의 전체 이벤트 시퀀스에서 파생됩니다. 이러한 필드는 보내지 않습니다. Adobe에서 생성합니다.

## Platform 데이터 세트에 작성하는 이벤트

추적할 수 있는 12개의 이벤트 유형 중 5개만 데이터 세트에 개별 경험 이벤트 쓰기를 생성합니다.

| 이벤트 유형 | 데이터 세트에 포함 | 참고 |
|---|---|---|
| [세션 시작](/help/implementation/events/session/session-start.md) | 예 | 세션이 초기화될 때 작성됨 |
| [광고 시작](/help/implementation/events/ads/ad-start.md) | 예 | 개별 광고가 시작될 때 작성됨 |
| [광고 완료](/help/implementation/events/ads/ad-complete.md) | 예 | 광고가 완료될 때까지 재생될 때 작성됨 |
| [챕터 완료](/help/implementation/events/chapters/chapter-complete.md) | 예 | 챕터가 완료될 때까지 재생될 때 작성됨 |
| [세션 완료](/help/implementation/events/session/session-complete.md) | 예 | 세션이 종료될 때 기록됨, 가장 풍부한 계산 필드 세트 |
| [재생](/help/implementation/events/playback/play.md) | 아니요 | `timePlayed`을(를) 계산하는 데 사용 |
| [시작 일시 중지](/help/implementation/events/playback/pause-start.md) | 아니요 | `pauseCount` 및 `pauseTime`을(를) 계산하는 데 사용 |
| [Ping](/help/implementation/events/playback/ping.md) | 아니요 | 하트비트, 세션 비활동을 감지하는 데 사용됩니다. |
| [버퍼 시작](/help/implementation/events/playback/buffer-start.md) | 아니요 | QoE 버퍼 지표를 계산하는 데 사용됩니다. |
| [비트율 변경](/help/implementation/events/playback/bitrate-change.md) | 아니요 | QoE 비트율 지표를 계산하는 데 사용됩니다. |
| [상태 시작](/help/implementation/events/player-state/state-start.md) | 아니요 | 플레이어 상태 지표를 계산하는 데 사용됨 |
| [오류](/help/implementation/events/error.md) | 아니요 | QoE에서 `errorCount`을(를) 계산하는 데 사용됨 |

## 백엔드 계산 필드

다음 필드는 `mediaReporting` 페이로드에 표시되지만 컬렉션 페이로드에는 포함되지 않습니다. 백엔드는 전체 이벤트 시퀀스에서 해당 이벤트를 파생합니다.

**세션 수준**(`sessionComplete`에 표시):

| 필드 | 설명 |
|---|---|
| `xdm.mediaReporting.sessionDetails.timePlayed` | 광고를 제외한 재생된 기본 콘텐츠의 총 시간(초) |
| `xdm.mediaReporting.sessionDetails.totalTimePlayed` | 광고를 포함하여 경과된 총 시간(초) |
| `xdm.mediaReporting.sessionDetails.uniqueTimePlayed` | 중복 제거된 시간(초). 두 번 이상 본 간격은 한 번만 카운트됩니다 |
| `xdm.mediaReporting.sessionDetails.averageMinuteAudience` | `timePlayed`을(를) 콘텐츠 길이로 나눈 값 |
| `xdm.mediaReporting.sessionDetails.estimatedStreams` | 예상 동시 스트림 |
| `xdm.mediaReporting.sessionDetails.adCount` | 시작된 광고 수 |
| `xdm.mediaReporting.sessionDetails.chapterCount` | 시작한 챕터 수 |
| `xdm.mediaReporting.sessionDetails.pauseCount` / `xdm.mediaReporting.sessionDetails.pauseTime` | 일시 중지 빈도 및 총 일시 중지 기간 |
| `xdm.mediaReporting.sessionDetails.hasProgress10` ... `xdm.mediaReporting.sessionDetails.hasProgress95` | 진행 마일스톤 플래그(10%, 25%, 50%, 75%, 95%) |
| `xdm.mediaReporting.sessionDetails.hasSegmentView` | 최소 1개 이상의 콘텐츠 프레임이 보였는지 여부 |
| `xdm.mediaReporting.sessionDetails.isCompleted` / `xdm.mediaReporting.sessionDetails.isPlayed` | 완료 및 시작 플래그 |
| `xdm.mediaReporting.sessionDetails.secondsSinceLastCall` | 마지막 ping과 세션 닫기 사이의 시간 |
| `xdm.mediaReporting.sessionDetails.segment` | 컨텐츠 세그먼트 대괄호(예: `[0-1]`) |

**광고 수준**(`adComplete`에 표시):

| 필드 | 설명 |
|---|---|
| `xdm.mediaReporting.advertisingDetails.timePlayed` | 광고 콘텐츠 재생 시간(초) |
| `xdm.mediaReporting.advertisingDetails.isCompleted` | 광고가 완료될 때까지 재생되었는지 여부 |

**챕터 수준**(`chapterComplete`에 표시):

| 필드 | 설명 |
|---|---|
| `xdm.mediaReporting.chapterDetails.timePlayed` | 챕터 콘텐츠 재생 시간(초) |
| `xdm.mediaReporting.chapterDetails.isCompleted` | 챕터가 끝까지 재생되었는지 여부 |
| `xdm.mediaReporting.chapterDetails.isStarted` | 챕터가 시작되었는지 여부 |

**QoE**(`sessionComplete`에 집계됨):

| 필드 | 설명 |
|---|---|
| `xdm.mediaReporting.qoeDataDetails.bitrateAverage` | 세션 간 평균 비트율 |
| `xdm.mediaReporting.qoeDataDetails.bitrateAverageBucket` | 버킷 평균 비트율 범위 |
| `xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` | 비트율 변경 수 |
| `xdm.mediaReporting.qoeDataDetails.errorCount` | 오류 수 |
| `xdm.mediaReporting.qoeDataDetails.droppedFrames` | 드롭된 총 프레임 수 |
| `xdm.mediaReporting.qoeDataDetails.playerSdkErrors` | 플레이어 오류 코드 배열 |
| `xdm.mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | 오류 발생 여부 |
| `xdm.mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | 드롭된 프레임 발생 여부 |
| `xdm.mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | 비트율 변경 발생 여부 |

## 다운로드한 컨텐츠

[다운로드한 끝점](/help/use-cases/track-downloaded-content.md)을 사용하여 추적한 세션의 경우 백엔드는 `sessionStart` 보고 이벤트에서 `xdm.mediaReporting.sessionDetails.isDownloaded`을(를) `true`(으)로 자동 설정합니다. 다운로드한 세션에 대한 다른 모든 보고 이벤트는 라이브 세션과 동일한 스키마를 따릅니다. CJA 또는 Adobe Analytics에서 이 필드를 사용하여 다운로드한 재생을 필터링하거나 세그먼트화합니다.

컬렉션 구현 세부 사항은 Media Edge API 참조의 [다운로드된 끝점](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/)을 참조하십시오.

## 구현 유효성 검사

Media Edge API를 통해 이벤트를 보낸 후 다음 방법 중 하나를 사용하여 데이터가 올바르게 도착했는지 확인합니다.

**Adobe Experience Platform 데이터 세트 미리 보기**

1. [CX Enterprise](https://experience.adobe.com)에서 **[!UICONTROL 데이터 세트]**(으)로 이동하여 스트리밍 미디어 데이터 세트를 선택하십시오.
2. 가장 최근에 수집된 경험 이벤트를 보려면 **[!UICONTROL 데이터 세트 미리 보기]**&#x200B;를 선택하십시오.
3. `media.sessionStart` 및 `media.sessionComplete`과(와) 같은 `eventType` 값이 채워진 `mediaReporting` 필드로 표시되는지 확인하십시오.

**Customer Journey Analytics 데이터 세트 검사**

1. CJA에서 스트리밍 미디어 데이터 세트와 연결된 연결을 엽니다.
2. **데이터 세트 추가**&#x200B;를 선택하고 스키마를 검사하여 `mediaReporting` 필드가 예상 차원 및 지표에 매핑되었는지 확인하십시오.

**Adobe Analytics 처리 규칙(Analytics 대상을 사용하는 경우)**

Analytics 소스 커넥터를 통해 데이터를 받는 Adobe Analytics 보고서 세트의 경우 처리 규칙을 사용하여 `mediaReporting` 컨텍스트 데이터 변수를 사용자 지정 속성 또는 eVar에 매핑할 수 있습니다. `isDownloaded` 플래그는 `a.media.downloaded`(으)로 사용할 수 있습니다.

## XDM 페이로드 예

다음 예제에서는 Platform 데이터 세트에 기록된 각 보고 이벤트에 대한 전체 `mediaReporting` XDM 구조를 보여 줍니다. `_{tenantName}` 속성은 사용자 지정 필드에 대한 조직의 테넌트 네임스페이스를 나타냅니다.

+++media.sessionStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "isViewed": true,
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "hasResume": false,
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionStart",
    "_id": "0[...]0",
    "timestamp": "YYYY-11-20T12:43:35Z"
  }
}
```

+++

+++media.adStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "name": "/uri-reference/001",
        "length": 10,
        "siteID": "siteID",
        "isStarted": true,
        "creativeID": "creativeID",
        "friendlyName": "Ad 1"
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adStart",
    "_id": "d[...]0",
    "timestamp": "YYYY-11-20T12:43:56Z"
  }
}
```

+++

+++media.adComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "length": 10,
        "creativeID": "creativeID",
        "timePlayed": 7,
        "name": "/uri-reference/001",
        "siteID": "siteID",
        "friendlyName": "Ad 1",
        "isCompleted": true
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adComplete",
    "_id": "f[...]0",
    "timestamp": "YYYY-11-20T12:44:03Z"
  }
}
```

+++

+++media.chapterComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2",
      "customTest": "myCustomValue1"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "chapterDetails": {
        "timePlayed": 10,
        "offset": 0,
        "length": 10,
        "index": 1,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "isStarted": true,
        "friendlyName": "Chapter 1",
        "isCompleted": true
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.chapterComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:24Z"
  }
}
```

+++

+++media.sessionComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "qoeDataDetails": {
        "playerSdkErrors": ["test-buffer-start"],
        "bitrateAverageBucket": "0-99",
        "bitrateChangeCount": 1,
        "droppedFrames": 30,
        "hasErrorImpactedStreams": true,
        "hasBitrateChangeImpactedStreams": true,
        "hasDroppedFrameImpactedStreams": true,
        "bitrateAverage": 35,
        "timeToStart": 1,
        "errorCount": 1
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "hasProgress10": true,
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "episode": "4933",
        "pauseTime": 3,
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "segment": "[0-1]",
        "season": "1521",
        "showType": "sitcom",
        "pauseCount": 1,
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "uniqueTimePlayed": 47,
        "totalTimePlayed": 55,
        "author": "test-author",
        "hasProgress25": true,
        "feed": "sourceFeed",
        "timePlayed": 48,
        "name": "test-name",
        "publisher": "test-media-publisher",
        "hasPauseImpactedStreams": true,
        "averageMinuteAudience": 0.48,
        "artist": "test-artist",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "hasSegmentView": true,
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "friendlyName": "test-friendly-name",
        "isCompleted": true,
        "playerName": "HTML5 player",
        "album": "test-album",
        "chapterCount": 1,
        "length": 100,
        "adCount": 1,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "secondsSinceLastCall": 51,
        "assetID": "/uri-reference",
        "isPlayed": true,
        "estimatedStreams": 1,
        "firstDigitalDate": "releaseDate"
      },
      "states": [
        {
          "isSet": true,
          "name": "mute",
          "count": 1,
          "time": 3
        },
        {
          "isSet": true,
          "name": "pictureInPicture",
          "count": 1,
          "time": 3
        }
      ]
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:40Z"
  }
}
```

+++

+++media.sessionStart (다운로드한 컨텐츠)

[다운로드한 끝점](/help/use-cases/track-downloaded-content.md)을(를) 사용하여 추적된 세션은 하나의 키 차이가 있는 동일한 보고 스키마를 따릅니다. `xdm.mediaReporting.sessionDetails.isDownloaded`은(는) `sessionStart` 보고 이벤트에서 `true`(으)로 설정되어 있습니다. 다른 모든 이벤트 유형은 위의 라이브 콘텐츠 예제와 동일합니다.

```json
{
  "xdm": {
    "mediaReporting": {
      "customMetadata": [
        {
          "name": "customData",
          "value": "example"
        }
      ],
      "playhead": 0,
      "sessionDetails": {
        "ID": "d8a25708a6b0be83975e32e2f422105ed62f51ff67e6d82d898657534ab9244f",
        "channel": "channel",
        "contentType": "VOD",
        "length": 100,
        "name": "123456789",
        "playerName": "playerName",
        "isDownloaded": true
      }
    },
    "eventType": "media.sessionStart",
    "timestamp": "YYYY-09-26T15:52:24Z",
    "identityMap": {
      "ECID": [
        {
          "id": "51910389753901685456014889838591030721"
        }
      ]
    },
    "implementationDetails": {
      "version": "0.0.1",
      "environment": "browser",
      "name": "https://ns.adobe.com/experience/edge"
    }
  }
}
```

+++
