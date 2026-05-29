---
title: JavaScript 3.x Media SDK API 참조
description: Media SDK JavaScript 3.x(ADB.Media 및 ADB.MediaConfig 클래스)에 대한 API 참조.
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3f8a2b5-1d4e-4f9a-8c7b-3a2d1f0e9b6c
source-git-commit: 1022e0851d58db0c9b523ebb7b52d379239a2e07
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 17%

---


# JavaScript 3.x Media SDK API 참조

>[!BEGINSHADEBOX]

이 페이지에서는 Analytics 전용 JavaScript 3.x SDK에 대해 설명합니다. 권장 구현은 [Edge Network을 사용하여 Streaming Media 구현](/help/implementation/edge/edge-web-sdk.md)을 참조하십시오.

>[!ENDSHADEBOX]

## ADB.Media

### 정적 메서드

+++구성

추적을 위해 MediaSDK를 구성합니다. 이 메서드는 페이지에서 추적기 인스턴스를 만들기 전에 한 번 호출해야 합니다.

**구문**

```javascript
ADB.Media.configure(mediaConfig, appMeasurement);
```

| 변수 이름 | 유형 | 설명 |
|---|---|---|
| `mediaConfig` | `ADB.MediaConfig` | 유효한 미디어 구성 |
| `appMeasurement` | 오브젝트 | AppMeasurement 인스턴스 |

**예**

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

+++

+++getInstance

재생 세션을 추적할 미디어 인스턴스를 만듭니다. 미디어를 구성하기 전에 호출되면 `null`을(를) 반환합니다.

**구문**

```javascript
ADB.Media.getInstance(trackerConfig)
```

| 변수 이름 | 유형 | 필수 여부 | 설명 |
| :--- | :--- | :---: | :--- |
| `trackerConfig` | 추적기 구성 | 아니요 | 추적기 구성 개체입니다. |

**예**

```javascript
var tracker = ADB.Media.getInstance();
```

추적기 인스턴스당 `channel` 또는 `playerName`을(를) 재정의하려면 추적기 구성 개체에 재정의 값을 전달하십시오.

**추적기 구성 예제**

```javascript
const trackerConfig = {
  [Media.TrackerConfig.Channel]: "custom_channel_name",
  [Media.TrackerConfig.PlayerName]: "custom_player_name",
}
this._mediaTracker = Media.getInstance(trackerConfig);
```

+++

+++create미디어 개체

미디어 정보가 포함된 개체를 만듭니다. 잘못된 매개 변수가 전달되면 빈 개체를 반환합니다.

**구문**

```javascript
ADB.Media.createMediaObject(name, id, length, streamType, mediaType)
```

| 변수 이름 | 유형 | 설명 |
| :--- | :--- | :--- |
| `name` | 문자열 | 미디어 이름을 나타내는 빈 문자열이 아닙니다. |
| `id` | 문자열 | 고유한 미디어 식별자를 나타내는 빈 문자열이 아닙니다. |
| `length` | 숫자 | 미디어의 길이(초)를 나타내는 양수입니다. 길이를 알 수 없는 경우 `0`을(를) 사용합니다. |
| `streamType` | 문자열 | 미디어 스트림 유형을 나타내는 스트림 유형 또는 빈 문자열이 아닙니다. |
| `mediaType` | 미디어 유형 | 미디어 유형(오디오 또는 비디오) |

**예**

```javascript
var mediaObject = ADB.Media.createMediaObject("video-name",
                                              "video-id",
                                              60.0,
                                              ADB.Media.StreamType.VOD,
                                              ADB.Media.MediaType.Video);
```

+++

+++createAdBreakObject

광고 브레이크 정보가 포함된 개체를 만듭니다. 잘못된 매개 변수가 전달되면 빈 개체를 반환합니다.

**구문**

```javascript
ADB.Media.createAdBreakObject(name, position, startTime);
```

| 변수 이름 | 유형 | 설명 |
| :--- | :--- | :--- |
| `name` | 문자열 | 광고 브레이크 이름(프리롤, 미드롤 및 포스트롤)을 나타내는 빈 문자열이 아닙니다. |
| `position` | 숫자 | 콘텐츠 내 광고 브레이크의 번호 위치로서, 1로 시작합니다. |
| `startTime` | 숫자 | 광고 브레이크의 시작 위치에 있는 플레이헤드 값입니다. |

**예**

```javascript
var adbreakObject = ADB.Media.createAdBreakObject("midroll", 2, 30.0);
```

+++

+++createAdObject

광고 정보가 포함된 개체를 만듭니다. 잘못된 매개 변수가 전달되면 빈 개체를 반환합니다.

**구문**

```javascript
ADB.Media.createAdObject(name, id, position, length);
```

| 변수 이름 | 유형 | 설명 |
| :--- | :--- | :--- |
| `name` | 문자열 | 광고 이름을 나타내는 빈 문자열이 아님 |
| `id` | 문자열 | 광고 ID를 나타내는 빈 문자열이 아님 |
| `position` | 숫자 | 광고 브레이크 내 광고 번호 위치로서 1로 시작합니다. |
| `length` | 숫자 | 광고 길이를 나타내는 양수입니다 |

**예**

```javascript
var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0)
```

+++

+++createChapterObject

챕터 정보가 포함된 개체를 만듭니다. 잘못된 매개 변수가 전달되면 빈 개체를 반환합니다.

**구문**

```javascript
ADB.Media.createChapterObject(name, position, length, startTime)
```

| 변수 이름 | 유형 | 설명 |
| :--- | :--- | :--- |
| `name` | 문자열 | 챕터 이름을 나타내는 빈 문자열이 아닙니다. |
| `position` | 숫자 | 콘텐츠 내에서 챕터의 위치로서, 1로 시작합니다. |
| `length` | 숫자 | 챕터 길이를 나타내는 양수입니다. |
| `startTime` | 숫자 | 챕터 시작 부분의 플레이헤드 값 |

**예**

```javascript
var chapterObject = ADB.Media.createChapterObject("name", 1, 30.0, 0)
```

+++

+++createStateObject

상태 정보를 포함하는 개체를 만듭니다. 잘못된 매개 변수가 전달되면 빈 개체를 반환합니다.

**구문**

```javascript
ADB.Media.createStateObject(name)
```

| 변수 이름 | 유형 | 설명 |
| :--- | :--- | :--- |
| `name` | 문자열 | 플레이어 상태 또는 상태 이름을 나타내는 빈 문자열이 아님 |

**예**

```javascript
var stateObject = ADB.Media.createStateObject("customstate");
```

+++

+++createQoEObject

QoE 정보가 포함된 개체를 만듭니다. 잘못된 매개 변수가 전달되면 빈 개체를 반환합니다.

**구문**

```javascript
ADB.Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)
```

| 변수 이름 | 유형 | 설명 |
| :--- | :--- | :--- |
| `bitrate` | 숫자 | 현재 비트율을 나타내는 양수(알 수 없는 경우 0) |
| `startupTime` | 숫자 | 시작 시간을 나타내는 양수(알 수 없는 경우 0) |
| `fps` | 숫자 | 현재 fps를 나타내는 양수(알 수 없는 경우 0) |
| `droppedFrames` | 숫자 | 드롭된 프레임 수를 나타내는 양수(알 수 없는 경우 0) |

**예**

```javascript
qoeObject = ADB.Media.createQoEObject(10000000, 2, 23, 10);
```

+++

+++version

MediaSDK 버전을 반환합니다.

**구문**

```javascript
ADB.Media.version
```

**예**

```javascript
console.log(ADB.Media.version);
```

+++

### 인스턴스 메서드

+++trackSessionStart

재생을 시작하려는 의도를 추적합니다. 이렇게 하면 미디어 추적기 인스턴스에서 추적 세션이 시작됩니다. 미디어 재개 도 참조하십시오.

**구문**

```javascript
ADB.Media.trackSessionStart(mediaObject, contextData);
```

| 변수 이름 | 설명 | 필수 여부 |
| :--- | :--- | :---: |
| `mediaObject` | `createMediaObject` 메서드를 사용하여 만든 미디어 정보입니다. | 예 |
| `contextData` | 선택적 미디어 컨텍스트 데이터. 표준 메타데이터 키의 경우 표준 비디오 상수 또는 표준 오디오 상수를 사용하십시오. | 아니요 |

**예**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[ADB.Media.VideoMetadataKeys.Show] = "Sample Show";
contextData["isUserLoggedIn"] = "false";
contextData["tvStation"] = "Sample TV Station";

tracker.trackSessionStart(mediaObject, contextData);
```

+++

+++trackPlay

이전 일시 중지 후 미디어 재생 또는 다시 시작을 추적합니다.

**구문**

```javascript
ADB.Media.trackPlay();
```

**예**

```javascript
tracker.trackPlay();
```

+++

+++trackPause

미디어 일시 중지를 추적합니다.

**구문**

```javascript
ADB.Media.trackPause();
```

**예**

```javascript
tracker.trackPause();
```

+++

+++trackComplete

미디어 추적 완료. 미디어를 완전히 본 경우에만 이 메서드를 호출합니다.

**구문**

```javascript
ADB.Media.trackComplete();
```

**예**

```javascript
tracker.trackComplete();
```

+++

+++trackSessionEnd

보기 세션의 끝을 추적합니다. 사용자가 완료할 미디어를 보지 않은 경우에도 이 메서드를 호출합니다.

**구문**

```javascript
ADB.Media.trackSessionEnd();
```

**예**

```javascript
tracker.trackSessionEnd();
```

+++

+++trackError

미디어 재생 중 오류를 추적합니다.

**구문**

```javascript
ADB.Media.trackError(errorId);
```

| 변수 이름 | 설명 | 필수 여부 |
| :--- | :--- | :---: |
| `errorId` | 오류 정보가 포함된 빈 문자열이 아닙니다. | 예 |

**예**

```javascript
tracker.trackError("errorId");
```

+++

+++trackEvent

미디어 이벤트를 추적하는 메서드입니다.

| 변수 이름 | 설명 |
| :--- | :--- |
| `event` | 미디어 이벤트 |
| `info` | `AdBreakStart` 이벤트의 경우 adbreak 정보는 `createAdBreakObject` 메서드를 사용하여 만들어집니다. `AdStart` 이벤트의 경우 광고 정보는 `createAdObject` 메서드를 사용하여 만들어집니다. `ChapterStart` 이벤트의 경우 `createChapterObject` 메서드를 사용하여 챕터 정보가 만들어집니다. `StateStart` 및 `StateEnd` 이벤트의 경우 `createStateObject` 메서드를 사용하여 상태 정보가 만들어집니다. 다른 이벤트에는 필요하지 않습니다. |
| `contextData` | `AdStart` 및 `ChapterStart` 이벤트에 대해 선택적 컨텍스트 데이터를 제공할 수 있습니다. 다른 이벤트에는 필요하지 않습니다. |

**구문**

```javascript
ADB.Media.trackEvent(event, info, contextData);
```

**예**

**AdBreak 추적**

```javascript
// AdBreakStart
  var adBreakObject = ADB.Media.createAdBreakObject("preroll", 1, 0)
  tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);

// AdBreakComplete
  tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
```

**광고 추적**

```javascript
// AdStart
  var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0);

  var adMetadata = {};
  // Standard metadata keys provided by adobe.
  adMetadata[ADB.Media.AdMetadataKeys.Advertiser]  ="Sample Advertiser";
  adMetadata[ADB.Media.AdMetadataKeys.CampaignId] = "Sample Campaign";
  // Custom metadata keys
  adMetadata["affiliate"] = "Sample affiliate";

  tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);

// AdComplete
  tracker.trackEvent(ADB.Media.Event.AdComplete);

// AdSkip
  tracker.trackEvent(ADB.Media.Event.AdSkip);
```

**챕터 추적**

```javascript
// ChapterStart
  var chapterObject = ADB.Media.createChapterObject("chapter-name", 1, 60.0, 15.0);

  var chapterMetadata = {};
  chapterMetadata["segmentType"] = "Sample segment type";

  tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);

// ChapterComplete
  tracker.trackEvent(ADB.Media.Event.ChapterComplete);

// ChapterSkip
  tracker.trackEvent(ADB.Media.Event.ChapterSkip);
```

**추적 상태**

```javascript
// StateStart (ex: Mute is switched on)
  var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
  tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);

// StateEnd (ex: Mute is switched off)
  tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```

**재생 이벤트 추적**

```javascript
// BufferStart
  tracker.trackEvent(ADB.Media.Event.BufferStart);

// BufferComplete
  tracker.trackEvent(ADB.Media.Event.BufferComplete);

// SeekStart
  tracker.trackEvent(ADB.Media.Event.SeekStart);

// SeekComplete
  tracker.trackEvent(ADB.Media.Event.SeekComplete);
```

**비트율 변경 추적**

```javascript
// If the new bitrate value is available provide it to the tracker.
  var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
  tracker.updateQoEObject(qoeObject);

// Bitrate change
  tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

+++

+++updatePlayhead

미디어 추적기에 현재 미디어 플레이헤드를 제공합니다. 정확한 추적을 위해 재생 중에 플레이헤드가 변경될 때마다 이 메서드를 호출합니다.

**구문**

```javascript
ADB.Media.updatePlayhead(time);
```

| 변수 이름 | 설명 |
| :--- | :--- |
| `time` | 현재 플레이헤드(초)입니다. Video-on-demand(VOD)의 경우 값은 미디어 항목의 시작 부분부터 초 단위로 지정됩니다. 라이브 스트리밍의 경우 플레이어가 콘텐츠 지속 시간에 대한 정보를 제공하지 않으면 해당 날짜의 자정(UTC) 이후 경과된 시간(초 수)으로 값을 지정할 수 있습니다. 참고: 진행률 마커를 사용할 경우 콘텐츠 지속 시간이 필요하며 플레이헤드는 0부터 시작하여 미디어 항목의 시작부터 초 단위로 업데이트해야 합니다. |

**예**

```javascript
tracker.updatePlayhead(13.3);

// For live streams
var UTCTimeInSeconds = Math.floor(Date.now() / 1000)
var timeFromMidnightInSecond = UTCTimeInSeconds % 86400

tracker.updatePlayhead(timeFromMidnightInSecond);
```

+++

+++updateQoEObject

미디어 추적기에 현재 QoE 정보를 제공합니다. 정확한 추적을 위해 미디어 플레이어가 업데이트된 QoE 정보를 제공할 때 이 메서드를 여러 번 호출하십시오.

**구문**

```javascript
ADB.Media.updateQoEObject(qoeObject);
```

| 변수 이름 | 설명 |
| :--- | :--- |
| `qoeObject` | `createQoEObject` 메서드를 사용하여 만든 현재 QoE 정보입니다. |

**예**

```javascript
var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
tracker.updateQoEObject(qoeObject);
```

+++

+++제거

추적기 인스턴스를 제거합니다.

**구문**

```javascript
ADB.Media.destroy();
```

**예**

```javascript
tracker.destroy();
```

+++

### 상수

+++추적기 구성

추적기 인스턴스별로 설정할 수 있는 구성 키를 정의합니다.

```javascript
ADB.Media.TrackerConfig = {
  Channel: "media.channel",
  PlayerName: "media.playerName"
}
```

+++

+++미디어 유형

현재 추적되는 미디어 유형을 정의합니다.

```javascript
ADB.Media.MediaType = {
  Video: "video",
  Audio: "audio"
}
```

+++

+++스트림 유형

현재 추적되는 콘텐츠의 스트림 유형을 정의합니다.

```javascript
ADB.Media.StreamType = {
  VOD: "vod",
  Live: "live",
  Linear: "linear",
  Podcast: "podcast",
  Audiobook: "audiobook",
  AOD: "aod"
}
```

+++

+++표준 메타데이터 키

`ADB.Media.VideoMetadataKeys`, `ADB.Media.AudioMetadataKeys` 및 `ADB.Media.AdMetadataKeys`에서 표준 메타데이터에 대한 컨텍스트 데이터 키 문자열을 제공합니다. 키 및 해당 보고 변수의 전체 목록에 대해서는 [표준 메타데이터 변수 참조](/help/implementation/variables/standard-metadata/show.md)를 참조하십시오.

+++

+++미디어 이벤트

추적 이벤트의 유형을 정의합니다.

```javascript
ADB.Media.Event = {
  AdBreakStart: "adBreakStart",
  AdBreakComplete: "adBreakComplete",
  AdStart: "adStart",
  AdComplete: "adComplete",
  AdSkip: "adSkip",
  ChapterStart: "chapterStart",
  ChapterComplete: "chapterComplete",
  ChapterSkip: "chapterSkip",
  SeekStart: "seekStart",
  SeekComplete: "seekComplete",
  BufferStart: "bufferStart",
  BufferComplete: "bufferComplete",
  BitrateChange: "bitrateChange",
  StateStart: "stateStart",
  StateEnd: "stateEnd"
}
```

+++

+++플레이어 상태

플레이어 상태 추적을 위한 표준 값을 정의합니다.

```javascript
ADB.Media.PlayerState = {
  FullScreen: "fullScreen",
  ClosedCaption: "closedCaptioning",
  Mute: "mute",
  PictureInPicture: "pictureInPicture",
  InFocus: "inFocus"
}
```

+++

+++미디어 재개

현재 추적 세션이 이전에 닫은 세션을 다시 시작하고 있음을 나타내는 상수입니다. 추적 세션을 시작할 때 이 정보를 제공해야 합니다.

**구문**

```javascript
ADB.Media.MediaObjectKey = {
  MediaResumed: "resumed"
}
```

**예**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

mediaObject[ADB.Media.MediaObjectKey.MediaResumed] = true;

tracker.trackSessionStart(mediaObject);
```

+++

## ADB.MediaConfig

| 키 | 필수 여부 | 설명 |
| :--- | :--- | :--- |
| `trackingServer` | 예 | 다운로드한 미디어 추적 데이터를 전송해야 하는 미디어 컬렉션 API 서버의 이름을 입력합니다. 이 정보를 받으려면 Adobe 계정 담당자에게 문의하십시오. |
| `channel` | 아니요 | 채널 이름 속성입니다. |
| `playerName` | 아니요 | 사용 중인 미디어 플레이어의 이름 |
| `appVersion` | 아니요 | 미디어 플레이어 애플리케이션/SDK 버전 입력 |
| `debugLogging` | 아니요 | 미디어 SDK 로그를 활성화하거나 비활성화합니다(기본값: `false`). |
| `ssl` | 아니요 | SSL을 통해 Ping을 보냅니다(기본값: `true`). |
