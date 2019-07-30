---
seo-title: 품질 매개 변수
title: 품질 매개 변수
uuid: 0 D 9 FA 764-EDEF -4178-8650-90 C 9 A 0852 A 57
translation-type: tm+mt
source-git-commit: 6e6ecdcb7309e06410a443247df5d5b49b083ea7

---


# 품질 매개 변수{#quality-parameters}

이 항목에서는 컨텍스트 데이터 값을 포함하여 Adobe에서 솔루션 변수를 통해 수집하는 QoE/QoS(체감 품질) 데이터의 목록을 제공합니다.

테이블 데이터 설명:

* **구현:**&#x200B;구현 값 및 요구 사항에 대한 정보
   * *키* - 앱에서 수동으로 설정하거나 Adobe Media SDK에 의해 자동으로 설정된 변수.
   * *필수* - 기본 비디오 추적에 매개 변수가 필요한지 여부를 나타냅니다.
   * *유형* - 설정할 변수의 유형(문자열 또는 숫자)을 지정합니다.
   * *보낸 날짜* - 데이터가 전송되는 시기를 나타냅니다. *미디어 시작은* 미디어 시작 시 전송된 분석 호출이고 *, 광고 시작은* 광고 시작 시 전송된 분석 호출입니다. *닫기* 호출은 하트비트 서버에서 미디어 세션이 끝날 때 Analytics 서버로 바로 전송되는 컴파일된 Analytics 호출이나 광고, 장 (chapter) 의 끝입니다. 네트워크 패킷 호출에서는 Close 호출을 사용할 수 없습니다.
   * *최소. SDK 버전* - 매개 변수에 액세스하는 데 필요한 SDK 버전을 나타냅니다.
   * *샘플 값* - 일반 변수 사용법 예를 제공합니다.
* **네트워크 매개 변수:** Adobe Analytics 또는 하트비트 서버에 전달되는 값을 표시합니다. 이 열에는 Adobe Media SDK에서 생성한 네트워크 호출에 표시되는 매개 변수의 이름이 표시됩니다.
* **보고:** 비디오 데이터를 보고 분석하는 방법에 대한 정보입니다.
   * *사용 가능* - 기본적으로 데이터를 보고할 수 있는지(*Yes*) 또는 사용자 지정 설정(*Custom*)이 필요한지 여부를 나타냅니다.
   * *예약된 변수* - 데이터가 예약된 변수의 이벤트, eVar, prop 또는 분류로 캡처되는지 여부를 나타냅니다.
   * *보고서 이름* - 변수에 대한 Adobe Aanlytics 보고서 이름
   * *컨텍스트 데이터* - 보고 서버에 전달되고 처리 규칙에 사용되는 Adobe Analytics 컨텍스트 데이터의 이름.
   * *데이터 피드* - 클릭스트림 또는 라이브 스트림 데이터 피드에서 찾은 변수의 열 이름
   * *Audience Manager* - Adobe Audience Manager에 있는 Trait 이름

## 품질 메타데이터 {#section_8467F9729DA04A888A2657712234D7C7}

### 평균 비트율

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **API 키:**<br/>media.qoe.bitrate </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **전송 시점:**<br/>닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 800-899 </li><li> **설명:**<br/>평균 비트 전송률 (kbps) 입니다. 이 값은 100kbps 간격으로 사전 정의된 버킷입니다. 평균 비트율은 재생 기간과 관련하여 재생 세션 중에 발생한 모든 비트율 값의 가중 평균으로 계산됩니다.에서 보냅니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>Bitrateaveragebucket) </li> <li> **하트비트:**<br/> (L: 스트림: 비트 전송률) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>평균 비트율 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>Bitrateaveragebucket) </li> <li> **데이터 피드:**<br/>videoqoebitrateaverageevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>Bitrateaveragebucket) </li> </ul> |



### 시작 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.qoe.timeToStart </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 30,000 </li><li> **설명:**<br/>Qosobject를 통해 설정하지 않으면 기본값이 0로 설정됩니다. 이 값의 설정 단위는 밀리초입니다. 값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>timeToStart) </li> <li> **하트비트:**<br/> (L: 스트림: startup_ time) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>시작 시간 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>timeToStart) </li> <li> **데이터 피드:**<br/>videoqoetimetostartevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>timeToStart) </li> </ul> |



### FPS

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.qoe.framesPerSecond </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 24 </li><li> **설명:**<br/>스트림 프레임 속도의 현재 값입니다 (초당 프레임 수).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **하트비트:**<br/> (L: 스트림: fps) </li> </ul> | <ul> <li> **사용 가능:**<br/>아니요 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/>N/A </li> <li> **컨텍스트 데이터:**<br/> </li> <li> **데이터 피드:**<br/> </li> <li> **Audience Manager:**<br/> </li> </ul> |



### 드롭된 프레임

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>droppedFrames </li> <li> **API 키:**<br/>media.qoe.droppedFrames </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 3 </li><li> **설명:**<br/>드롭된 프레임 (정수) 의 수입니다. 이 값은 재생 세션 중에 드롭된 모든 프레임의 합계로 계산됩니다. 이 값은 (l: 스트림: dropped_ frames).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>Droppedframecount) </li> <li> **하트비트:**<br/> (L: 스트림:<br/>dropped_ frames) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>삭제된 프레임 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>Droppedframecount) </li> <li> **데이터 피드:**<br/>videoqoedroppedframecountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>Droppedframecount) </li> </ul> |



### 버퍼 이벤트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 2 </li><li> **설명:**<br/>버퍼 이벤트 수입니다. 이 지표는 재생 세션 중에 발생한 다른 버퍼 상태의 수로 계산됩니다. 플레이어가 다른 상태에서 버퍼 상태에 들어가는 횟수입니다(예: 재생 또는 일시 정지).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>Buffercount) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = buffer) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>버퍼 이벤트 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>Buffercount) </li> <li> **데이터 피드:**<br/>videoqoebuffercountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>Buffercount) </li> </ul> |



### 총 버퍼 지속 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:** </li> <li> **샘플 값:**<br/> 30 </li><li> **설명:**<br/>버퍼링이 소요된 총 시간 (초) 입니다. 이 값은 재생 세션 중에 발생한 모든 버퍼 이벤트 기간의 합계로 계산됩니다. 값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다. <br/>**릴리스 날짜: 2018년 9월 13일**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>Buffertime) </li> <li> **하트비트:**<br/> (L: 이벤트: 지속 기간) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>총 버퍼 지속 시간 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>Buffertime) </li> <li> **데이터 피드:**<br/>videoqoebuffertimeevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>Buffertime) </li> </ul> |



### 비트율 변경

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.qoe.bitrateChange </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 3 </li><li> **설명:**<br/>비트 전송률 변경 사항 (정수) 의 수입니다. 이 값은 재생 세션 중에 발생한 모든 비트율 변경 이벤트의 합계로 계산됩니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>Bitratechangecount) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>비트율 변경 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>Bitratechangecount) </li> <li> **데이터 피드:**<br/>videoqoebitratechangecountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>Bitratechangecount) </li> </ul> |



### 오류/오류 이벤트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/> </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 1 </li><li> **설명:**<br/>발생한 오류 수입니다 (정수). 이 값은 재생 세션 중에 발생한 모든 오류 이벤트의 합계로 계산됩니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>Errorcount) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = error) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>오류 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>Errorcount) </li> <li> **데이터 피드:**<br/>videoqoeerrorcountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>Errorcount) </li> </ul> |



### 플레이어 SDK 오류 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/> </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>플레이어 SDK에서 생성된 고유한 오류 ID 고객은 제공된 오류 API를 통해 구현 시 오류 코드/ID를 제공해야 합니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>Playersdkerrors) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = error) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>오류 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>Playersdkerrors) </li> <li> **데이터 피드:**<br/> Videoqoeplayersdkerrors </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>Playersdkerrors) </li> </ul> |



### 외부 오류 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/> </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>외부 소스의 고유 오류 ID (예: CDN 오류). 고객은 제공된 오류 API를 통해 구현 시 오류 코드/ID를 제공해야 합니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>Externalerrors) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = error) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>오류 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>Externalerrors) </li> <li> **데이터 피드:**<br/> Videoqoeextneralerrors </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>Externalerrors) </li> </ul> |



### Media SDK 오류 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/> </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>재생하는 동안 Media SDK에서 생성된 고유한 오류 ID 입니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>Mediasdkerrors) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = error) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>오류 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>Mediasdkerrors) </li> <li> **데이터 피드:** <br/>mediaqoeexternalerrors </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>Mediasdkerrors) </li> </ul> |




### 세션 종료 {#session-end}

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/> </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:** 2.1 </li> <li> **샘플 값:**<br/> end </li><li> **설명:**<br/>종료 이벤트는 SDK가 백엔드에 대한 close 호출을 보내고 있음을 의미합니다. 이 이벤트를 수신하면 백엔드가 이 비디오에 대한 세션을 닫고 추가 처리를 수행하지 않습니다. <br/>미디어가 100%까지 완료되면 관련 정보를 보려면 `s:event:type=complete.`[컨텐츠 완료](audio-video-parameters.md#content-complete) 후 이 메시지를 보내야 합니다. </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트 비트:**<br/> (s: 이벤트: type = end) </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>N/A </li> <li> **컨텍스트 데이터:**<br/> </li> <li> **데이터 피드:**<br/> </li> <li> **Audience Manager:**<br/> </li> </ul> |



## 품질 지표 {#section_8EB0C9CBC09340C8915E1D2707D0A9EE}

### 시작 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 30,000 </li><li> **설명:**<br/>Qosobject를 통해 설정하지 않으면 기본값이 0로 설정됩니다. 이 값의 설정 단위는 밀리초입니다. 값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다. <br/>**릴리스 날짜: 2018년 9월 13일**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>timeToStart) </li> <li> **하트비트:**<br/> (L: 스트림: startup_ time) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>시작 시간 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>timeToStart) </li> <li> **데이터 피드:**<br/>videoqoetimetostart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>timeToStart) </li> </ul> |



### 버퍼 이벤트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 2 </li><li> **설명:**<br/>버퍼 이벤트 (정수) 의 수입니다. 이 지표는 재생 세션 중에 발생한 버퍼 이벤트 수로 계산됩니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>Buffercount) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = buffer) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>버퍼 이벤트 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>Buffercount) </li> <li> **데이터 피드:**<br/>videoqoebuffercount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>Buffercount) </li> </ul> |



### 총 버퍼 지속 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 15 </li><li> **설명:**<br/>총 체류 시간 버퍼링 (초; 정수). 이 값은 재생 세션 중에 발생한 모든 버퍼 이벤트 기간의 합계로 계산됩니다. 값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다. <br/>**릴리스 날짜: 2018년 9월 13일**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>Buffertime) </li> <li> **하트비트:**<br/> (L: 이벤트: 지속 기간) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>총 버퍼 지속 시간 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>Buffertime) </li> <li> **데이터 피드:**<br/>videoqoebuffertime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>Buffertime) </li> </ul> |



### 비트율 변경

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>이벤트 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> " 3 " </li><li> **설명:**<br/>비트 전송률 변경의 수입니다. 이 값은 재생 세션 중에 발생한 모든 비트율 변경 이벤트의 합계로 계산됩니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>Bitratechangecount) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>비트율 변경 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>Bitratechangecount) </li> <li> **데이터 피드:**<br/>videoqoebitratechangecount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>Bitratechangecount) </li> </ul> |



### 오류

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 1 </li><li> **설명:**<br/>발생한 오류 수 (정수). 이 값은 재생 세션 중에 발생한 모든 오류 이벤트의 합계로 계산됩니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>Errorcount) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = error) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>오류 이벤트 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>Errorcount) </li> <li> **데이터 피드:**<br/>videoqoeerrorcount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>Errorcount) </li> </ul> |



### 드롭된 프레임

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 1 </li><li> **설명:**<br/>드롭된 프레임 수 (정수). 이 값은 재생 세션 중에 드롭된 모든 프레임의 합계로 계산됩니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>Droppedframecount) </li> <li> **하트비트:**<br/> (L: 스트림:<br/>dropped_ frames) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>삭제된 프레임 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>Droppedframecount) </li> <li> **데이터 피드:**<br/>videoqoedroppedframecount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>Droppedframecount) </li> </ul> |



### 시작 전 드롭

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> true </li><li> **설명:**<br/>시작하기 전에 사용자가 비디오를 종료하는 횟수입니다. 이 지표는 광고에 관계없이 컨텐츠가 렌더링되지 않은 경우에만 1로 설정됩니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>Dropbeforestart) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = aa_ start) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>시작 전 드롭 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>Dropbeforestart) </li> <li> **데이터 피드:**<br/>videoqoedropbeforestart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>Dropbeforestart) </li> </ul> |



>[!IMPORTANT]
>이 이벤트가 설정되어 있으면 가능한 유일한 값은 true 입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.

### 버퍼 영향을 받은 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> true </li><li> **설명:**<br/>버퍼링에 영향을 받는 스트림의 수입니다. 이 지표는 재생 세션 중에 하나 이상의 버퍼 이벤트가 발생한 경우에만 1로 설정됩니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>buffer) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = buffer) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>버퍼 영향을 받은 스트림 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>buffer) </li> <li> **데이터 피드:**<br/>videoqoebuffer </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>이 이벤트가 설정되어 있으면 가능한 유일한 값은 true 입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.

### 비트율 변경의 영향을 받은 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> true </li><li> **설명:**<br/>비트 전송률 변경이 발생한 스트림의 수입니다. 이 지표는 재생 세션 중에 하나 이상의 비트율 변경 이벤트가 발생한 경우에만 1로 설정됩니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>Bitratechange) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/> 영향을 받은 스트림 변경 사항 스트림 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>Bitratechange) </li> <li> **데이터 피드:**<br/>videoqoebitratechange </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>Bitratechange) </li> </ul> |



>[!IMPORTANT]
>이 이벤트가 설정되어 있으면 가능한 유일한 값은 true 입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.

### 평균 비트율

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 3200 </li><li> **설명:**<br/>평균 비트 전송률 (kbps, 정수) 입니다. 이 지표는 재생 기간과 관련하여 재생 세션 중에 발생한 모든 비트율 값의 가중 평균으로 계산됩니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>bitrateaverage) </li> <li> **하트비트:**<br/> (L: 스트림: 비트 전송률) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>평균 비트율 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>bitrateaverage) </li> <li> **데이터 피드:**<br/>videoqoebitrateaverage </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>bitrateaverage) </li> </ul> |



### 오류 영향을 받은 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> true </li><li> **설명:**<br/>오류 이벤트가 발생한 스트림 수 (즉, 재생 세션 중에 `trackError` 호출되었고 `type=error` 하트비트 호출이 생성되었음). </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>라는 오류가 표시됩니다) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = error) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>오류 영향을 받은 스트림 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>라는 오류가 표시됩니다) </li> <li> **데이터 피드:**<br/>videoqoeerror </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>라는 오류가 표시됩니다) </li> </ul> |



>[!IMPORTANT]
>이 이벤트가 설정되어 있으면 가능한 유일한 값은 true 입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.

### 드롭된 프레임 영향을 받은 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> true </li><li> **설명:**<br/>프레임이 드롭된 스트림의 수입니다. 이 지표는 재생 세션 중에 하나 이상의 프레임이 드롭된 경우에만 1로 설정됩니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>droppedFrames) </li> <li> **하트비트:**<br/> (L: 스트림:<br/>dropped_ frames) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>드롭된 프레임 영향을 받은 스트림 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>droppedFrames) </li> <li> **데이터 피드:**<br/>videoqoedroppedframes </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>droppedFrames) </li> </ul> |



>[!IMPORTANT]
>이 이벤트가 설정되어 있으면 가능한 유일한 값은 true 입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.

### 지연 영향을 받은 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5+ </li> <li> **샘플 값:**<br/> true </li><li> **설명:**<br/>지연된 이벤트가 발생한 스트림의 수입니다. 이 지표는 재생 중에 하나 이상의 정지가 발생한 경우에만 1로 설정됩니다. 고객이 보고에 사용할 수 있는 값을 갖도록 고유한 처리 규칙을 만들어야 합니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>stall) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = stall) </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/> </li> <li> **데이터 피드:**<br/>N/A </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>stall) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>stall) </li> </ul> |



>[!IMPORTANT]
>이 이벤트가 설정되어 있으면 가능한 유일한 값은 true 입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.

### 지연 이벤트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5+ </li> <li> **샘플 값:**<br/> " 3 " </li><li> **설명:**<br/>재생 세션 중에 재생이 지연된 횟수입니다. 고객이 보고에 사용할 수 있는 값을 갖도록 고유한 처리 규칙을 만들어야 합니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>stallcount) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = stall) </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/> </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>stallcount) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>stallcount) </li> </ul> |



### 총 지연 기간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5+ </li> <li> **샘플 값:**<br/> 12 </li><li> **설명:**<br/>총 시간 (초; 정수 재생 세션 중에 재생이 정지되었습니다. 고객이 보고에 사용할 수 있는 값을 갖도록 고유한 처리 규칙을 만들어야 합니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. qoe.<br/>Stalltime) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = stall) </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/> </li> <li> **컨텍스트 데이터:**<br/> (a. Media. qoe.<br/>Stalltime) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. qoe.<br/>Stalltime) </li> </ul> |



## Related APIs {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

