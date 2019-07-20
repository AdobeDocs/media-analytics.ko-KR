---
seo-title: 1.x에서 2.x API로 전환
title: 1.x에서 2.x API로 전환
uuid: 6 E 619288-C 082-4 CB 4-8685-E 90823 DADF 4 A
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# API 1.x to 2.x conversion {#one-x-to-two-x-conv}

## Media SDK 2. x API 참조

* [Android API 참조](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/index.html)
* [iOS API 참조](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/index.html)
* [JS API 참조](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html)
* [Chromecast API 참조](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/index.html)

## 필수 트랙 * API:

| VHL 1. x  | VHL 2. x |
|---|---|
| `videoPlayerPlugin.trackVideoLoad()` | 해당 없음 |
| `videoPlayerPlugin.trackSessionStart()` | [mediaHeartbeat.trackSessionStart(mediaObject, mediaCustomMetadata)](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionStart) |
| `videoPlayerPlugin.trackPlay()` | [mediaHeartbeat.trackPlay()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPlay) |
| `videoPlayerPlugin.trackPause()` | [mediaHeartbeat.trackPause()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPause) |
| `videoPlayerPlugin.trackComplete()` | [mediaHeartbeat.trackComplete()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackComplete) |
| `videoPlayerPlugin.trackVideoUnload()` | [mediaHeartbeat.trackSessionEnd()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionEnd) |
| `videoPlayerPlugin.trackApplicationError()` | 해당 없음 |
| `videoPlayerPlugin.trackVideoPlayerError()` | [mediaHeartbeat.trackError()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackError) |

이제 광고, 챕터, 비트율 변경, 찾기 및 버퍼링과 같은 선택적 추적 API는 모두 단일 `trackEvent` API의 일부입니다. [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackEvent) API는 추적하려는 이벤트 유형을 나타내는 상수 매개 변수를 수신합니다.

## 선택적 trackEvent API:

| VHL 1.x | VHL 2.x |
|---|---|
| Return a valid `AdBreakInfo` in `VideoPlayerPlugin.getAdBreakInfo()` | `trackEvent(Event.AdBreakStart)` |
| Return null in `VideoPlayerPlugin.getAdBreakInfo()` | `trackEvent(Event.AdBreakComplete)` |
| `playerPlugin.trackAdStart()` | `trackEvent(Event.AdStart, adObject, adCustomMetadata)` |
| `playerPlugin.trackAdComplete()` | `trackEvent(Event.AdComplete)` |
| Return null in `VideoPlayerPlugin.getAdInfo()` | `trackEvent(Event.AdSkip)` |
| `playerPlugin.trackChapterStart()` | `trackEvent(Event.ChapterStart, chapterObject, chapterCustomMetadata)` |
| `playerPlugin.trackChapterComplete()` | `trackEvent(Event.ChapterComplete)` |
| Return null in `VideoPlayerPlugin.getChapterInfo()` | `trackEvent(Event.ChapterSkip)` |
| `playerPlugin.trackSeekStart()` | `trackEvent(Event.SeekStart)` |
| `playerPlugin.trackSeekComplete()` | `trackEvent(Event.SeekComplete)` |
| `playerPlugin.trackBufferStart()` | `trackEvent(Event.BufferStart)` |
| `playerPlugin.trackBufferComplete()` | `trackEvent(Event.BufferComplete)` |
| `playerPlugin.trackBitrateChange()` | `trackEvent(Event.BitrateChange)` |
| `playerPlugin.trackTimedMetadata()` | `trackEvent(Event.TimedMetadataUpdate)` |

