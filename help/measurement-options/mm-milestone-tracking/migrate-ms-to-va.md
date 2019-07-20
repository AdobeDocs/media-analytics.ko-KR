---
seo-title: 이정표에서 Media Analytics로의 마이그레이션
title: 이정표에서 Media Analytics로의 마이그레이션
uuid: FDC 96146-AF 63-48 CE-B 938-C 0 CA 70729277
translation-type: tm+mt
source-git-commit: 27740fc1753e8ac9cf5a4b240a56b1c2dd567010

---


# 이정표에서 Media Analytics로의 마이그레이션 {#migrating-from-milestone-to-media-analytics}

## 개요 {#section_ihl_nbz_cfb}

비디오 측정의 핵심 개념은 이정표 추적과 Media Analytics 추적에 대해 동일하며, 이러한 추적에서는 비디오 플레이어 이벤트를 가져와서 이를 분석 메서드에 매핑하고, 플레이어 메타데이터 및 값도 가져와서 분석 변수에 매핑합니다. Media Analytics 솔루션은 이정표에서 발전된 것이므로 많은 메서드와 지표가 동일하지만 구성 접근 방식과 코드는 크게 변경되었습니다. 새로운 Media Analytics 메서드를 가리키도록 플레이어 이벤트 코드를 업데이트할 수 있어야 합니다. See [SDK Overview](../../sdk-implement/setup/setup-overview.md) and [Tracking Overview](../../sdk-implement/track-av-playback/track-core-overview.md) for more details on implementing Media Analytics.

다음 표는 이정표 솔루션과 Media Analytics 솔루션 간의 변환 내용을 제공합니다.

## 마이그레이션 안내 {#section_iyb_pbz_cfb}

### 변수 참조

| 이정표 지표 | 변수 유형 | Media Analytics 지표 |
| --- | --- | --- |
| 컨텐츠 | eVar<br/><br/>Default expiration: Visit | 컨텐츠 |
| 컨텐츠 유형 | eVar<br/><br/> Default expiration: Page view | 컨텐츠 유형 |
| 컨텐츠 체류 시간 | Event<br/><br/> Type: Counter | 컨텐츠 체류 시간 |
| 비디오 시작 | Event<br/><br/> Type: Counter | 비디오 시작 |
| 비디오 완료 | 이벤트<br/><br/> 유형:카운터 | 컨텐츠 완료 |

### 미디어 모듈 변수

<table>
<thead>
<tr>
<th>이정표
</th>
<th>이정표 구문
</th>
<th>Media Analytics
</th>
<th>Media Analytics 구문
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
s.Media.trackUsingContextData = true;
</pre>
</td>
<td>해당 없음
</td>
<td>모든 Media Analytics 데이터는 컨텍스트 데이터를 사용해서만 전송됩니다.
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
<td>Media Analytics 컨텍스트 데이터가 예약된 변수에 자동으로 채워집니다. eVar, prop 및 이벤트에 대한 매핑은 구현 코드 내에 더 이상 필요하지 않습니다. 고객은 처리 규칙을 사용하여 컨텍스트 데이터를 변수에 매핑할 수 있습니다.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s. Media. trackvars = 
 " events,
 prop 2,
 evar 1,
 evar 2,
 evar 3 ";
</pre>
</td>
<td>해당 없음
</td>
<td>예약된 변수 및 처리 규칙을 통해 매핑이 수행되므로 더 이상 필요하지 않습니다.
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s. Media. trackevents = 
 " event 1,
 event 2,
 event 3,
 event 4,
 event 5,
 event 6,
 event 7 "
</pre>
</td>
<td>해당 없음
</td>
<td>예약된 변수 및 처리 규칙을 통해 매핑이 수행되므로 더 이상 필요하지 않습니다.
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
<th>Media Analytics
</th>
<th>Media Analytics 구문
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
<td>미리 만들어진 플레이어 매핑은 더 이상 제공되지 않습니다.
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.
  Autotracknetstreams
 = true
</pre>
</td>
<td>해당 없음
</td>
<td>미리 만들어진 플레이어 매핑은 더 이상 제공되지 않습니다.
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.
  Completebycloseoffset
 = true
</pre>
</td>
<td>해당 없음
</td>
<td>컨텐츠 완료는 100% 진행률 마커만 지원합니다.
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
<td>컨텐츠 완료는 100% 진행률 마커만 지원합니다.
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
SDK 키: playername; 
API 키: media. playername
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</p>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.
  Trackseconds
 = 15
</pre>
</td>
<td>해당 없음
</td>
<td>Media Analytics는 컨텐츠에 대해서는 10초, 광고에 대해서는 1초로 설정되어 있습니다. 다른 선택 사항은 없습니다.
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.
  trackmilestones
 = "25,50,75";
</pre>
</td>
<td>해당 없음
</td>
<td>Media Analytics는 항상 10%, 25%, 50%, 75%, 95%의 진행률 마커를 추적합니다.
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  Trackoffsetmilestones
 = "20,40,60";
</pre>
</td>
<td>해당 없음
</td>
<td>Media Analytics는 항상 10%, 25%, 50%, 75%, 95%의 진행률 마커를 추적합니다.
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
<td>자동 추적을 더 이상 사용할 수 없습니다.
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
<td>자동 추적을 더 이상 사용할 수 없습니다.
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
<th>Media Analytics
</th>
<th>Media Analytics 구문
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
s.Media.
  Adtrackseconds
 = 15
</pre>
</td>
<td>해당 없음
</td>
<td>Media Analytics는 컨텐츠에 대해서는 10초, 광고에 대해서는 1초로 설정되어 있습니다. 다른 선택 사항은 없습니다.
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.
  Adtrackmilestones
 = "25,50,75";
</pre>
</td>
<td>해당 없음
</td>
<td>진행률 마커는 기본적으로 광고에는 제공되지 않습니다. 광고 진행률 마커를 작성하려면 계산된 지표를 사용하십시오.
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
<td>Media Analytics는 광고에 대해서는 1초로 설정되어 있습니다. 다른 선택 사항은 없습니다.
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
<td>자동 추적을 더 이상 사용할 수 없습니다.
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
<td>자동 추적을 더 이상 사용할 수 없습니다.
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
<th>Media Analytics
</th>
<th>Media Analytics 구문
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.open
</td>
<td>
<pre>
s.Media.open(mediaName,mediaLength,mediaPlayerName)
</pre>
</td>
<td>
<pre>
trackSessionStart
</pre>
</td>
<td>
<pre>
Tracksessionstart (mediaobject, 
 Contextdata)
</pre>
</td>
</tr>
<tr>
<td>
Medianame - (필수) 비디오 보고서에 표시할 비디오의 이름입니다.
</td>
<td>
<pre>
mediaName
</pre>
</td>
<td>
<pre>
이름
</pre>
</td>
<td>
<pre>
Createmediaobject (name, 
 Mediaid, 
 length, 
 Streamtype)
</pre>
</td>
</tr>
<tr>
<td>
Medialength - (필수) 비디오의
길이 (초).
</td>
<td>
<pre>
mediaLength
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
Createmediaobject (name, 
 Mediaid, 
 length, 
 Streamtype)
</pre>
</td>
</tr>
<tr>
<td>
Mediaplayername - (필수) 비디오 보고서에 표시되기를 원하는 경우 비디오를 보는 데 사용되는 미디어 플레이어의 이름입니다.
</td>
<td>
<pre>
mediaPlayerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
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
<td>
<pre>
Trackevent
</pre>
</td>
<td>
<pre>
Mediaheartbeat. trackevent (mediaheartbeat.
 이벤트.
    Adbreakstart, 
 Adbreakobject);
...
Trackevent (mediaheartbeat.
 이벤트.
    Adstart, 
 Adobject, 
 Adcustommetadata);
</pre>
</td>
</tr>
<tr>
<td>
이름 - (필수) 광고의 이름 또는 ID 입니다.
</td>
<td>
<pre>
이름
</pre>
</td>
<td>
<pre>
이름
</pre>
</td>
<td>
<pre>
Createadobject (name, 
 Adid, 
 위치, 
 길이)
</pre>
</td>
</tr>
<tr>
<td>
길이
(필수) 광고의 길이입니다.
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
Createadobject (name, 
 Adid, 
 위치, 
 길이)
</pre>
</td>
</tr>
<tr>
<td>
Playername - (필수) 광고를 보는 데 사용되는 미디어
플레이어의 이름입니다.
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
Parentname - 광고가 포함된 기본 컨텐트의 이름 또는 ID 입니다.
</td>
<td>
<pre>
parentName
</pre>
</td>
<td>해당 없음
</td>
<td>자동 상속됨
</td>
</tr>
<tr>
<td>
Parentpod - 광고가 재생되는 기본 컨텐츠에서의 위치입니다.
</td>
<td>
<pre>
parentPod
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
Createadbreakobject (name, 
 위치, 
 Starttime)
</pre>
</td>
</tr>
<tr>
<td>
Parentpodposition - 광고가 재생되는 창 내에서의 위치입니다.
</td>
<td>
<pre>
parentPodPosition
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
Createadobject (name, 
 Adid, 
 위치, 
 길이)
</pre>
</td>
</tr>
<tr>
<td>
이 재생에 적용되는 CPM 또는 암호화된 CPM (" ~" 접두사가 붙은 CPM) 를 CPM
합니다.
</td>
<td>
<pre>
CPM
</pre>
</td>
<td>해당 없음
</td>
<td>미디어 분석에서는 기본적으로 사용할 수 없습니다.
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
<td>해당 없음
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
<td>
<pre>
trackSessionEnd
</pre>
</td>
<td>
<pre>
trackSessionEnd()
</pre>
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
<pre>
trackComplete
</pre>
</td>
<td>
<pre>
trackComplete()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.play
</pre>
</td>
<td>
<pre>
s.Media.play(name,offset,segmentNum,segment, segmentLength)
</pre>
</td>
<td>
<pre>
trackPlay
</pre>
</td>
<td>
<pre>
trackPlay()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.stop
</pre>
</td>
<td>
<pre>
s.Media.stop(mediaName,mediaOffset)
</pre>
</td>
<td>
<pre>
trackPause
</pre> 또는  
<pre>
Trackevent
</pre>
</td>
<td>
<pre>
trackPause()
</pre> 
또는 
<pre>
Trackevent (mediaheartbeat.
 이벤트.
  SeekStart)
</pre> 또는 
<pre>
Trackevent (mediaheartbeat.
 이벤트.
  BufferStart);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.monitor
</pre>
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>추가적인 변수를 설정하려면 사용자 지정 또는 표준 메타데이터를 사용하십시오.
</td>
<td>
<pre>
var customvideometadata = 
{isuserloggedin: 
 " false ",
 tvstation: 
 " 샘플 TV 방송국 ",
 프로그래머: 
 " Sample Programmer "};
...
var standardvideometadata 
 = {};
Standardvideometadata
 [mediaheartbeat.
 VideoMetadataKeys.
   에피소드] = 
 " Sample 에피소드 ";
Standardvideometadata
 [mediaheartbeat.
 VideoMetadataKeys.
   show] = "Sample Show";
...
Mediaobject. setvalue (mediaheartbeat.
 Mediaobjectkey.
 Standardvideometadata, 
 Standardvideometadata);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.track
</pre>
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>해당 없음
</td>
<td>추적 호출 빈도가 자동으로 설정됩니다.
</td>
</tr>
</tbody>
</table>

