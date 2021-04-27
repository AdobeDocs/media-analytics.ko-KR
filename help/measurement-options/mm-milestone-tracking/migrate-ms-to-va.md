---
title: 이정표에서 Media Analytics로의 마이그레이션
description: 이정표에서 Media Analytics로의 마이그레이션
uuid: fdc96146-af63-48ce-b938-c0ca70729277
exl-id: 655841ed-3a02-4e33-bbc9-46fb14302194
translation-type: ht
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: ht
source-wordcount: '675'
ht-degree: 100%

---

# 이정표에서 Media Analytics로의 마이그레이션 {#migrating-from-milestone-to-media-analytics}

## 개요 {#overview}

비디오 측정의 핵심 개념은 이정표 및 Media Analytics에도 동일하며, 이러한 추적에서는 비디오 플레이어 이벤트를 가져와서 이를 분석 메서드에 매핑하고, 플레이어 메타데이터 및 값도 가져와서 분석 변수에 매핑합니다. Media Analytics 솔루션은 이정표에서 발전된 것이므로 많은 메서드와 지표가 동일하지만 구성 접근 방식과 코드는 크게 변경되었습니다. 새로운 Media Analytics 메서드를 가리키도록 플레이어 이벤트 코드를 업데이트할 수 있어야 합니다. Media Analytics 구현에 대한 자세한 내용은 [SDK 개요](/help/sdk-implement/setup/setup-overview.md) 및 [추적 개요](/help/sdk-implement/track-av-playback/track-core-overview.md)를 참조하십시오.

다음 표는 이정표 솔루션과 Media Analytics 솔루션 간의 변환 내용을 제공합니다.

## 마이그레이션 안내 {#migration-guide}

### 변수 참조

| 이정표 지표 | 변수 유형 | Media Analytics 지표 |
| --- | --- | --- |
| 콘텐츠 | eVar <br>기본 만료: 방문 | 콘텐츠 |
| 콘텐츠 유형 | eVar <br>기본 만료: 페이지 보기 | 콘텐츠 유형 |
| 콘텐츠 체류 시간 | 이벤트 <br>유형: 카운터 | 콘텐츠 체류 시간 |
| 비디오 시작 | 이벤트 <br>유형: 카운터 | 비디오 시작 |
| 비디오 완료 | 이벤트 <br>유형: 카운터 | 콘텐츠 완료 |


### 미디어 모듈 변수

| 이정표 | 이정표 구문 | Media Analytics | Media Analytics 구문 |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | 해당 없음 | 모든 Media Analytics 데이터는 컨텍스트 데이터를 사용해서만 전송됩니다. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | 해당 없음 | Media Analytics 컨텍스트 데이터가 예약된 변수에 자동으로 채워집니다. eVar, prop 및 이벤트에 대한 매핑은 구현 코드 내에 더 이상 필요하지 않습니다. 고객은 처리 규칙을 사용하여 컨텍스트 데이터를 변수에 매핑할 수 있습니다. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | 해당 없음 | 예약된 변수 및 처리 규칙을 통해 매핑이 수행되므로 더 이상 필요하지 않습니다. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | 해당 없음 | 예약된 변수 및 처리 규칙을 통해 매핑이 수행되므로 더 이상 필요하지 않습니다. |

### 선택 사항 변수

| 이정표 | 이정표 구문 | Media Analytics | Media Analytics 구문 |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | 해당 없음 | 미리 만들어진 플레이어 매핑은 더 이상 제공되지 않습니다. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | 해당 없음 | 미리 만들어진 플레이어 매핑은 더 이상 제공되지 않습니다. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | 해당 없음 | 콘텐츠 완료는 100% 진행률 마커만 지원합니다. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | 해당 없음 | 콘텐츠 완료는 100% 진행률 마커만 지원합니다. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | SDK 키: playerName;<br> API 키: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | 해당 없음 | Media Analytics는 콘텐츠에 대해서는 10초, 광고에 대해서는 1초로 설정되어 있습니다. 다른 선택 사항은 없습니다. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | 해당 없음 | Media Analytics는 항상 10%, 25%, 50%, 75%, 95%의 진행률 마커를 추적합니다.. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | 해당 없음 | Media Analytics는 항상 10%, 25%, 50%, 75%, 95%의 진행률 마커를 추적합니다.. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | 해당 없음 | 자동 추적을 더 이상 사용할 수 없습니다.. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | 해당 없음 | 자동 추적을 더 이상 사용할 수 없습니다.. |

### 광고 추적 변수

| 이정표 | 이정표 구문 | Media Analytics | Media Analytics 구문 |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | 해당 없음 | Media Analytics는 콘텐츠에 대해서는 10초, 광고에 대해서는 1초로 설정되어 있습니다. 다른 선택 사항은 없습니다. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | 해당 없음 | 진행률 마커는 기본적으로 광고에는 제공되지 않습니다. 광고 진행률 마커를 작성하려면 계산된 지표를 사용하십시오. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | 해당 없음 | Media Analytics는 광고에 대해서는 1초로 설정되어 있습니다. 다른 선택 사항은 없습니다. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | 해당 없음 | 자동 추적을 더 이상 사용할 수 없습니다.. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | 해당 없음 | 자동 추적을 더 이상 사용할 수 없습니다.. |

### 미디어 모듈 메서드

| 이정표 | 이정표 구문 | Media Analytics | Media Analytics 구문 |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName | `mediaName`: (필수) 비디오 보고서에 나타낼 비디오 이름입니다. | 이름 | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength | `mediaLength`: (필수) 비디오 길이(초)입니다. | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName | `mediaPlayerName`: (필수) 비디오를 보는 데 사용되는 미디어 플레이어의 이름으로 비디오 보고서에 나타나도록 할 이름입니다. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| 이름 | `name`: (필수) 광고 이름 또는 ID입니다. | 이름 | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length | `length`: (필수) 광고 길이입니다. | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName | `playerName`: (필수) 광고를 보는 데 사용되는 미디어 플레이어의 이름입니다. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName | `parentName`: 광고가 포함된 기본 콘텐츠의 이름 또는 ID입니다. | 해당 없음 | 자동 상속됨. |
| parentPod | `parentPod`: 기본 콘텐츠에서 광고가 재생되는 위치입니다. | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition | `parentPodPosition`: Pod 내에서 광고가 재생되는 위치입니다. | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM | `CPM`: 이 재생에 적용되는 CPM 또는 암호화된 CPM(앞에 &quot;~&quot;가 붙음)입니다. | 해당 없음 | 기본적으로 Media Analytics에서 사용할 수 없음. |
| Media.click | `s.Media.click(name, offset)` | 해당 없음 | 사용자 지정 링크 분석 호출을 사용하여 클릭 수를 추적하십시오. |
| Media.close | `s.Media.close(mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(name, offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(mediaName, mediaOffset)` | trackPause<br> 또는 <br>trackEvent | `trackPause()`<br> 또는 `trackEvent(`<br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)`<br> 또는 <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | 추가적인 변수를 설정하려면 사용자 지정 또는 표준 메타데이터를 사용하십시오. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(mediaName)` | 해당 없음 | 추적 호출 빈도가 자동으로 설정됩니다. |
