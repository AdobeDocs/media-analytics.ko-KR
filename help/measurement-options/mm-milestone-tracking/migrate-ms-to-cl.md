---
title: 이정표에서 사용자 지정 링크로의 마이그레이션에 대해 알아봅니다.
description: 이정표 변수를 사용자 지정 링크로, 이정표 모듈 메서드를 사용자 지정 링크 구문으로 변환하는 방법에 대해 알아봅니다.
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
exl-id: 732079f4-3eb8-4b9a-892b-25a1c9332be4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 100%

---

# 이정표에서 사용자 지정 링크로의 마이그레이션{#migrating-from-milestone-to-custom-link}

## 개요 {#overview}

이정표 추적과 사용자 지정 링크 추적에서 비디오 측정의 핵심 개념은 동일합니다. 이 추적에서는 비디오 플레이어 이벤트를 가져와서 분석 메서드에 매핑하는 동시에 플레이어 메타데이터 및 값도 가져와서 분석 변수에 매핑합니다. 사용자 지정 링크 접근 방식은 구현과 수집된 데이터에서 불필요한 항목을 제거하여 모두 간소화한 것으로 간주해야 합니다. 사용자 지정 링크 솔루션을 사용하면 비디오 측정을 위해 미리 정의된 변수나 메서드가 없으므로 전체 사용자 지정 설정이 필요합니다. 시작 및 완료와 같은 기본 플레이어 이벤트에 대한 사용자 지정 링크 추적 호출을 가리키도록 플레이어 이벤트 코드를 업데이트할 수 있어야 합니다. 자세한 내용은 [사용자 지정 링크 구현 안내서](/help/measurement-options/cl-in-aa/cl-impl-guide.md)를 참조하십시오.

다음 표는 이정표 솔루션과 사용자 지정 링크 솔루션 간의 변환 내용을 제공합니다.

## 마이그레이션 안내 {#migration-guide}

### 비디오 변수 참조

| 이정표 지표 | 변수 유형 | 사용자 지정 링크 |
| --- | --- | --- |
| 콘텐츠 | eVar <br>기본 만료: 방문 | 자신만의 eVar를 정의하십시오. |
| 콘텐츠 유형 | eVar <br>기본 만료: 페이지 보기 | 자신만의 eVar를 정의하십시오. |
| 콘텐츠 체류 시간 | 이벤트 <br>유형: 카운터 | 자신만의 이벤트를 정의하십시오. |
| 비디오 시작 | 이벤트 <br>유형: 카운터 | 자신만의 이벤트를 정의하십시오. |
| 비디오 완료 | 이벤트 <br>유형: 카운터 | 자신만의 이벤트를 정의하십시오. |

### 미디어 모듈 변수

| 이정표 | 이정표 구문 | 사용자 지정 링크 | 사용자 지정 링크 구문 |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `  contextData.video.name’;` <br> `  s.contextData["video.name"]` <br> `  = mediaName;` |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | 해당 없음 | 이제 처리 규칙을 통해 eVar, prop 및 이벤트에 컨텍스트 데이터를 매핑하는 작업이 완료됩니다. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `    prop10,` <br> `    eVar10,` <br> `    eVar12,` <br> `    eVar13,` <br> `    eVar15,` <br> `    contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | linkTrackEvents | `s.linkTrackEvents` <br> `  = 'event2';` |

### 선택 사항 변수

| 이정표 | 이정표 구문 | 사용자 지정 링크 | 사용자 지정 링크 구문 |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | 해당 없음 | 사용할 수 없음. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | 해당 없음 | 사용할 수 없음. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | 해당 없음 | 사용할 수 없음. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | 해당 없음 | 사용할 수 없음. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | 링크 호출에서 eVar 또는 컨텍스트 데이터 변수를 설정합니다. | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | 해당 없음 | 사용할 수 없음. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | 해당 없음 | 사용할 수 없음. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | 해당 없음 | 사용할 수 없음. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | 해당 없음 | 사용할 수 없음. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | 해당 없음 | 사용할 수 없음. |

### 광고 추적 변수

| 이정표 | 이정표 구문 | 사용자 지정 링크 | 사용자 지정 링크 구문 |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | 해당 없음 | 사용할 수 없음. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | 해당 없음 | 사용할 수 없음. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | 해당 없음 | 사용할 수 없음. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | 해당 없음 | 사용할 수 없음. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | 해당 없음 | 사용할 수 없음. |

### 미디어 모듈 메서드

| 이정표 | 이정표 구문 | 사용자 지정 링크 | 사용자 지정 링크 구문 |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.view';` <br> `s.linkTrackEvents ` <br> `  = 'event2';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event2';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.view']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Start');` |
| mediaName | `mediaName`: (필수) 비디오 보고서에 나타낼 비디오 이름입니다. | 링크 호출에서 eVar 또는 컨텍스트 데이터 변수를 설정합니다. | `s.prop10 = mediaName;` <br> `s.eVar10 = mediaName;` <br> `s.contextData['video.name']` <br> `  = mediaName;` |
| mediaLength | `mediaLength`: (필수) 비디오 길이(초)입니다. | 링크 호출에서 eVar 또는 컨텍스트 데이터 변수를 설정합니다. | `s.contextData['video.length']` <br> `  = ”90”;` |
| mediaPlayerName | `mediaPlayerName`: (필수) 비디오를 보는 데 사용되는 미디어 플레이어의 이름으로 비디오 보고서에 나타나도록 할 이름입니다. | 링크 호출에서 eVar 또는 컨텍스트 데이터 변수를 설정합니다. | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | 해당 없음 | 사용할 수 없음. |
| 이름 | `name`: (필수) 광고 이름 또는 ID입니다. | 해당 없음 | 사용할 수 없음. |
| length | `length`: (필수) 광고 길이입니다. | 해당 없음 | 사용할 수 없음. |
| playerName | `playerName`: (필수) 광고를 보는 데 사용되는 미디어 플레이어의 이름입니다. | 해당 없음 | 사용할 수 없음. |
| parentName | `parentName`: 광고가 포함된 기본 콘텐츠의 이름 또는 ID입니다. | 해당 없음 | 사용할 수 없음. |
| parentPod | `parentPod`: 기본 콘텐츠에서 광고가 재생되는 위치입니다. | 해당 없음 | 사용할 수 없음. |
| parentPodPosition | `parentPodPosition`: Pod 내에서 광고가 재생되는 위치입니다. | 해당 없음 | 사용할 수 없음. |
| CPM | `CPM`: 이 재생에 적용되는 CPM 또는 암호화된 CPM(앞에 &quot;~&quot;가 붙음)입니다. | 해당 없음 | 사용할 수 없음. |
| Media.click | `s.Media.click(name, offset)` | `s.tl()` | 사용자 지정 링크 분석 호출을 사용하여 클릭 수를 추적하십시오. |
| Media.close | `s.Media.close(mediaName)` | 해당 없음 | 사용할 수 없음. |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.complete';` <br> `s.linkTrackEvents ` <br> `  = 'event3';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event3';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.complete']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Complete');` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | 해당 없음 | 사용할 수 없음. |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | 해당 없음 | 사용할 수 없음. |
| Media.monitor | `s.Media.monitor(s, media)` | 링크 호출에서 eVar 또는 컨텍스트 데이터 변수를 설정합니다. | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> `s.linkTrackEvents = 'event2';` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | 해당 없음 | 사용할 수 없음. |
