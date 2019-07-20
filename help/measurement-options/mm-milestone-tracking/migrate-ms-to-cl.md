---
seo-title: 이정표에서 사용자 지정 링크로의 마이그레이션
title: 이정표에서 사용자 지정 링크로의 마이그레이션
uuid: 1 c 8 edde 5-0 ef 1-4 bc 0-a 62 d -1747 f 4907 f 09
translation-type: tm+mt
source-git-commit: 530973abc12fcb2567a3742c202d992944048b8b

---


# 이정표에서 사용자 지정 링크로의 마이그레이션{#migrating-from-milestone-to-custom-link}

## 개요 {#section_xlc_fc2_dfb}

이정표 추적과 사용자 지정 링크 추적에서 비디오 측정의 핵심 개념은 동일합니다. 이 추적에서는 비디오 플레이어 이벤트를 가져와서 분석 메서드에 매핑하는 동시에 플레이어 메타데이터 및 값도 가져와서 분석 변수에 매핑합니다. 사용자 지정 링크 접근 방식은 구현과 수집된 데이터에서 불필요한 항목을 제거하여 모두 간소화한 것으로 간주해야 합니다. 사용자 지정 링크 솔루션을 사용하면 비디오 측정을 위해 미리 정의된 변수나 메서드가 없으므로 전체 사용자 지정 설정이 필요합니다. 시작 및 완료와 같은 기본 플레이어 이벤트에 대한 사용자 지정 링크 추적 호출을 가리키도록 플레이어 이벤트 코드를 업데이트할 수 있어야 합니다. 자세한 내용은 [사용자 지정 링크 구현 안내서](../../measurement-options/cl-in-aa/cl-impl-guide.md) 및 [사용자 지정 링크 코드를 사용하여 수동으로 링크 추적](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html)을 참조하십시오.

다음 표는 이정표 솔루션과 사용자 지정 링크 솔루션 간의 변환 내용을 제공합니다.

## 마이그레이션 안내 {#section_btt_fc2_dfb}

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
<p>이벤트</p>
<p>유형:카운터</p>
</td>
<td>자신만의 이벤트를 정의하십시오.</td>
</tr>
<tr>
<td>비디오 시작</td>
<td>
<p>이벤트</p>
<p>유형:카운터</p>
</td>
<td>자신만의 이벤트를 정의하십시오.</td>
</tr>
<tr>
<td>비디오 완료</td>
<td>
<p>이벤트</p>
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
  Trackusingcontextdata 
 = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 =' events, 
contextdata. video. name '; 
s. contextdata [' video. name ']
 = medianame;
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
  Contextdatamapping = {"a. Media. Name":
 " evar 2, prop 2 ","
 a. media. segment ":
 " Evar 3 ","
 a. contenttype ":
 " Evar 1 ","
 a. Media. timeplayed ":
 " event 3 ","
 a. media. view ":
 " event 1 ","
 a. media. segmentview ":
 " event 2 ","
 a. media. complete ":
 " event 7 ","
 a. media. milestone ": {25: " event 4 ",
 50: " event 5 ",
 75: " event 6 "}};
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
s. Media. trackvars
 = "events,
 prop 2,
 evar 1,
 evar 2,
 evar 3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 13,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. view ';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s. Media. trackevents
 = "event 1,
 event 2,
 event 3,
 event 4,
 event 5,
 event 6,
 event 7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s. linktrackevents
 =' event 2 ';
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
  Trackusingcontextdata 
 = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 =' events, 
contextdata. video. name '; 
s. contextdata [' video. name ']
 = medianame;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s. Media. contextdatamapping = {"a. Media. name": " evar 2, prop 2 ","
 a. media. segment ": " Evar 3 ","
 a. contenttype ": " Evar 1 ","
 a. Media. timeplayed ": " event 3 ","
 a. media. view ": " event 1 ","
 a. media. segmentview ": " event 2 ","
 a. media. complete ": " event 7 ","
 a. media. milestone ": {25: " event 4 ",
 50: " event 5 ",
 75: " event 6 "}};
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
s. Media. trackvars
 = "events,
 prop 2,
 evar 1,
 evar 2,
 evar 3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 13,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. view ';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s. Media. trackevents
 = "event 1,
 event 2,
 event 3,
 event 4,
 event 5,
 event 6,
 event 7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s. linktrackevents
 =' event 2 ';
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
  Completecloseoffsetthreshold
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
s. contextdata [' video. player ']
 =» customplayer Name»;
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
  Segmentbyoffsetmilestones
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
  Adtrackoffsetmilestones 
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
  Adsegmentbymilestones
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
  Adsegmentbyoffsetmilestones
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
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 15,
 contextdata. video. name,
 contextdata. video. view ';
s. linktrackevents 
 =' event 2 ';
s. prop 10 
 = Medianame;
s. evar 10 
 = Medianame;
s. evar 12 
 = "video";
s. evar 15 
 = Mediaplayername;
s. events 
 =' event 2 ';
s. contextdata [' video. name '] 
 = Medianame;
s. contextdata [' video. view '] 
 =' true ';
s. tl (this,' o ',' Video Start ');
</pre>
</td>
</tr>
<tr>
<td>mediaName</td>
<td><b>Medianame:</b> (필수) 비디오 보고서에 표시할 비디오의 이름입니다.</td>
<td>링크 호출에서 eVar 또는 컨텍스트 데이터 변수를 설정합니다.</td>
<td>
<pre>
s. prop 10 = medianame;
s. evar 10 = medianame;
s. contextdata [' video. name ']
 = medianame;
</pre>
</td>
</tr>
<tr>
<td>
mediaLength
</td>
<td>
<b>Medialength:</b> (필수) 비디오의 길이 (단위: 초)
</td>
<td>
링크 호출에서 eVar 또는 컨텍스트 데이터 변수를 설정합니다.
</td>
<td>
<pre>
s. contextdata [' video. length ']
 =» 90»;
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName
</td>
<td>
<b>Mediaplayername:</b> (필수) 비디오
보고서에 표시되기 원하는 방식으로 비디오를 보는 데 사용되는 미디어 플레이어의
이름입니다.
</td>
<td>
링크 호출에서 eVar 또는 컨텍스트 데이터 변수를 설정합니다.
</td>
<td>
<pre>
s. contextdata [' video. player ']
 =» customplayer Name»;
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
<td><b>이름:</b> (필수) 광고의 이름 또는 ID 입니다.</td>
<td>해당 없음</td>
<td>사용할 수 없음</td>
</tr>
<tr>
<td>
length
</td>
<td>
<b>길이:</b> (필수) 광고의 길이입니다.
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
<b>playername:</b> (필수) 광고를 보는 데 사용되는
미디어 플레이어의 이름입니다.
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
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. complete ';
s. linktrackevents 
 =' event 3 ';
s. prop 10 
 = Medianame;
s. evar 10 
 = Medianame;
s. evar 12 
 = "video";
s. evar 15 
 = Mediaplayername;
s. events 
 =' event 3 ';
s. contextdata [' video. name ']
 = medianame;
s. contextdata [' video. complete ']
 =' true ';
s. tl (this,' o ',' video complete ');
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
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. view ';
s. linktrackevents =' event 2 ';
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

