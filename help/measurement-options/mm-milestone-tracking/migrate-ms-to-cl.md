---
title: 이정표에서 사용자 지정 링크로의 마이그레이션
description: null
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# 이정표에서 사용자 지정 링크로의 마이그레이션{#migrating-from-milestone-to-custom-link}

## 개요 {#overview}

이정표 추적과 사용자 지정 링크 추적에서 비디오 측정의 핵심 개념은 동일합니다. 이 추적에서는 비디오 플레이어 이벤트를 가져와서 분석 메서드에 매핑하는 동시에 플레이어 메타데이터 및 값도 가져와서 분석 변수에 매핑합니다. 사용자 지정 링크 접근 방식은 구현과 수집된 데이터에서 불필요한 항목을 제거하여 모두 간소화한 것으로 간주해야 합니다. 사용자 지정 링크 솔루션을 사용하면 비디오 측정을 위해 미리 정의된 변수나 메서드가 없으므로 전체 사용자 지정 설정이 필요합니다. 시작 및 완료와 같은 기본 플레이어 이벤트에 대한 사용자 지정 링크 추적 호출을 가리키도록 플레이어 이벤트 코드를 업데이트할 수 있어야 합니다. 자세한 내용은 [사용자 지정 링크 구현 안내서](/help/measurement-options/cl-in-aa/cl-impl-guide.md) 및 [사용자 지정 링크 코드를 사용하여 수동으로 링크 추적](https://docs.adobe.com/content/help/en/media-analytics/using/measurement-options/cl-in-aa/cl-impl-guide.html)을 참조하십시오.

다음 표는 이정표 솔루션과 사용자 지정 링크 솔루션 간의 변환 내용을 제공합니다.

## 마이그레이션 안내 {#migration-guide}

### 비디오 변수 참조

<table>
<thead>
<tr>
<th><strong>이정표 지표</strong></th>
<th><strong>변수 유형</strong></th>
<th><strong>사용자 지정 링크</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>컨텐츠</td>
<td>
<p>eVar</p>
<p>기본 만료: 방문</p>
</td>
<td>자신만의 eVar를 정의하십시오.</td>
</tr>
<tr>
<td>컨텐츠 유형</td>
<td>
<p>eVar</p>
<p>기본 만료: 페이지 보기</p>
</td>
<td>자신만의 eVar를 정의하십시오.</td>
</tr>
<tr>
<td>컨텐츠 체류 시간</td>
<td>
<p>Event</p>
<p>유형:카운터</p>
</td>
<td>자신만의 이벤트를 정의하십시오.</td>
</tr>
<tr>
<td>비디오 시작</td>
<td>
<p>Event</p>
<p>유형:카운터</p>
</td>
<td>자신만의 이벤트를 정의하십시오.</td>
</tr>
<tr>
<td>비디오 완료</td>
<td>
<p>Event</p>
<p>유형:카운터</p>
</td>
<td>자신만의 이벤트를 정의하십시오.</td>
</tr>
</tbody>
</table>

### 미디어 모듈 변수

<table>
<thead>
<tr>
<th>이정표
</th>
<th>이정표 구문
</th>
<th>사용자 지정 링크
</th>
<th>사용자 지정 링크 구문
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.trackUsingContextData
</td>
<td>
<pre>
s.Media.
  trackUsingContextData 
  = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events, 
contextData.video.name’; 
s.contextData[‘video.name']
  = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.
  contextDataMapping = {
  "a.media.name":
    "eVar2,prop2",
  "a.media.segment":
    "eVar3",
  "a.contentType":
    "eVar1",
  "a.media.timePlayed":
    "event3",
  "a.media.view":
    "event1",
  "a.media.segmentView":
    "event2",
  "a.media.complete":
    "event7",
  "a.media.milestones":{
    25:"event4",
    50:"event5",
    75:"event6"
  }
};
</pre>
</td>
<td>해당 없음
</td>
<td>이제 처리 규칙을 통해 eVar, prop 및 이벤트에 컨텍스트 데이터를 매핑하는 작업이 완료됩니다.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars
  = "events,
     prop2,
     eVar1,
     eVar2,
     eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar13,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents
  = "event1,
     event2,
     event3,
     event4,
     event5,
     event6,
     event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents
  = 'event2';
</pre>
</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th>이정표
</th>
<th>이정표 구문
</th>
<th>사용자 지정 링크
</th>
<th>사용자 지정 링크 구문
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.trackUsingContextData
</td>
<td>
<pre>
s.Media.
  trackUsingContextData 
  = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events, 
contextData.video.name’; 
s.contextData[‘video.name']
  = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = {
  "a.media.name":"eVar2,prop2",
  "a.media.segment":"eVar3",
  "a.contentType":"eVar1",
  "a.media.timePlayed":"event3",
  "a.media.view":"event1",
  "a.media.segmentView":"event2",
  "a.media.complete":"event7",
  "a.media.milestones":{
    25:"event4",
    50:"event5",
    75:"event6"
  }
};
</pre>
</td>
<td>해당 없음
</td>
<td>이제 처리 규칙을 통해 eVar, prop 및 이벤트에 컨텍스트 데이터를 매핑하는 작업이 완료됩니다.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars
  = "events,
     prop2,
     eVar1,
     eVar2,
     eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar13,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents
  = "event1,
     event2,
     event3,
     event4,
     event5,
     event6,
     event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents
  = 'event2';
</pre>
</td>
</tr>
</tbody>
</table>

### 선택 사항 변수

<table>
<thead>
<tr>
<th>이정표
</th>
<th>이정표 구문
</th>
<th>사용자 지정 링크
</th>
<th>사용자 지정 링크 구문
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.autoTrack
</td>
<td>
<pre>
s.Media.autoTrack = true;
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.autoTrackNetStreams = true
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.completeByCloseOffset = true
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
Media.completeCloseOffsetThreshold
</td>
<td>
<pre>
s.Media.
  completeCloseOffsetThreshold
    = 1
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
Media.playerName
</td>
<td>
<pre>
s.Media.playerName = "Custom Player Name"
</pre>
</td>
<td>
링크 호출에서 eVar 또는 컨텍스트 데이터 변수를 설정합니다.
</td>
<td>
<pre>
s.contextData['video.player']
  = ”CustomPlayer Name”;
</pre>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.trackSeconds = 15
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.trackMilestones = "25,50,75";
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.trackOffsetMilestones = "20,40,60";
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
Media.segmentByMilestones
</td>
<td>
<pre>
s.Media.segmentByMilestones = true;
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
Media.segmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  segmentByOffsetMilestones
    = true;
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
</tbody>
</table>

### 광고 추적 변수

<table>
<thead>
<tr>
<th>이정표
</th>
<th>이정표 구문
</th>
<th>사용자 지정 링크
</th>
<th>사용자 지정 링크 구문
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.adTrackSeconds
</td>
<td>
<pre>
s.Media.adTrackSeconds = 15 
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.adTrackMilestones = "25,50,75";
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
Media.adTrackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adTrackOffsetMilestones 
    = "20,40,60";
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
Media.adSegmentByMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByMilestones
    = true;
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
Media.adSegmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByOffsetMilestones
    = true;
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
</tbody>
</table>

### 미디어 모듈 메서드

<table>
<thead>
<tr>
<th>이정표
</th>
<th>이정표 구문
</th>
<th>사용자 지정 링크
</th>
<th>사용자 지정 링크 구문
</th>
</tr>
</thead>
<tbody>
<tr>
<td>Media.open</td>
<td>
<pre>
s.Media.open(mediaName,mediaLength,mediaPlayerName)
</pre>
</td>
<td>s.tl()</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.video.name,
     contextData.video.view';
s.linkTrackEvents 
  = 'event2';
s.prop10 
  = mediaName;
s.eVar10 
  = mediaName;
s.eVar12 
  = "video";
s.eVar15 
  = mediaPlayerName;
s.events 
  = 'event2';
s.contextData['video.name'] 
  = mediaName;
s.contextData['video.view'] 
  = 'true';
s.tl(this,'o','Video Start');
</pre>
</td>
</tr>
<tr>
<td>mediaName</td>
<td><b>mediaName:</b> (필수) 비디오 보고서에 나타낼 비디오 이름입니다.</td>
<td>링크 호출에서 eVar 또는 컨텍스트 데이터 변수를 설정합니다.</td>
<td>
<pre>
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.contextData['video.name']
  = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
mediaLength
</td>
<td>
<b>mediaLength:</b> (필수) 비디오 길이(초)입니다.
</td>
<td>
링크 호출에서 eVar 또는 컨텍스트 데이터 변수를 설정합니다.
</td>
<td>
<pre>
s.contextData['video.length']
  = ”90”;
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName
</td>
<td>
<b>mediaPlayerName:</b> (필수) 비디오를 보는 데 사용되는
미디어 플레이어의 이름으로 비디오 보고서에 나타나도록 할 이름입니다.
</td>
<td>
링크 호출에서 eVar 또는 컨텍스트 데이터 변수를 설정합니다.
</td>
<td>
<pre>
s.contextData['video.player']
  = ”CustomPlayer Name”;
</pre>
</td>
</tr>
<tr>
<td>
Media.openAd
</td>
<td>
<pre>
s.Media.openAd(name,length,playerName,parentName,parentPod,parentPodPosition,CPM)
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음</td>
</tr>
<tr>
<td>이름</td>
<td><b>name:</b> (필수) 광고 이름 또는 ID입니다.</td>
<td>해당 없음</td>
<td>사용할 수 없음</td>
</tr>
<tr>
<td>
length
</td>
<td>
<b>length:</b> (필수) 광고 길이입니다.
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
playerName
</td>
<td>
<b>playerName:</b> (필수) 광고를 보는 데 사용되는 미디어 
플레이어의 이름입니다.
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
parentName
</td>
<td>
<b>parentName:</b> 광고가 포함된 기본 컨텐츠의 이름 또는 ID입니다.
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
parentPod
</td>
<td>
<b>parentPod:</b> 기본 컨텐츠에서 광고가 재생되는 위치입니다.
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
parentPodPosition
</td>
<td>
<b>parentPodPosition:</b> Pod 내에서 광고가 재생되는 위치입니다.
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
CPM
</td>
<td>
<b>CPM:</b> 이 재생에 적용되는 CPM 또는 암호화된 CPM(앞에 "~"가 붙음)입니다.
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click(name,offset)
</pre>
</td>
<td>
<pre>
s.tl()
</pre>
</td>
<td>사용자 지정 링크 분석 호출을 사용하여 클릭 수를 추적하십시오.
</td>
</tr>
<tr>
<td>
Media.close
</td>
<td>
<pre>
s.Media.close(mediaName)
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
Media.complete
</td>
<td>
<pre>
s.Media.complete(name,offset)
</pre>
</td>
<td>
s.tl()
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.complete';
s.linkTrackEvents 
  = 'event3';
s.prop10 
  = mediaName;
s.eVar10 
  = mediaName;
s.eVar12 
  = "video";
s.eVar15 
  = mediaPlayerName;
s.events 
  = 'event3';
s.contextData['video.name']
 =  mediaName;
s.contextData['video.complete']
 = 'true';
s.tl(this,'o','Video Complete');
</pre>
</td>
</tr>
<tr>
<td>
Media.play
</td>
<td>
<pre>
s.Media.play(name,offset,segmentNum,segment, segmentLength)
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
Media.stop
</td>
<td>
<pre>
s.Media.stop(mediaName,mediaOffset)
</pre>
</td>
<td>해당 없음 
</td>
<td>사용할 수 없음
</td>
</tr>
<tr>
<td>
Media.monitor
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>
링크 호출에서 eVar 또는 컨텍스트 데이터 변수를 설정합니다.
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.view';
s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
<tr>
<td>
Media.track
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>해당 없음
</td>
<td>사용할 수 없음
</td>
</tr>
</tbody>
</table>

