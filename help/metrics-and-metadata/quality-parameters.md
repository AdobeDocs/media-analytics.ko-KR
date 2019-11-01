---
title: 품질 매개 변수
description: null
uuid: 0d9fa764-edef-4178-8650-90c9a0852a57
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 품질 매개 변수{#quality-parameters}

이 항목에서는 컨텍스트 데이터 값을 포함하여 Adobe에서 솔루션 변수를 통해 수집하는 QoE/QoS(체감 품질) 데이터의 목록을 제공합니다.

테이블 데이터 설명:

* **구현:**&#x200B;구현 값 및 요구 사항에 대한 정보
   * *키* - 앱에서 수동으로 설정하거나 Adobe Media SDK에 의해 자동으로 설정된 변수.
   * *필수* - 기본 비디오 추적에 매개 변수가 필요한지 여부를 나타냅니다.
   * *유형* - 설정할 변수의 유형(문자열 또는 숫자)을 지정합니다.
   * *전송 대상* - 데이터가 전송될 시기를 나타냅니다.Media *Start* 는 미디어 시작 시 전송되는 분석 호출이며, *광고* 시작은 광고 시작 시 전송되는 분석 호출입니다.닫기 *호출은* 하트비트 서버에서 미디어 세션 종료 시 또는 광고 종료, 장 등 분석 서버로 직접 전송되는 컴파일된 분석 호출입니다. 닫기 호출은 네트워크 패킷 호출에서 사용할 수 없습니다.
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

## 품질 메타데이터 {#quality-metadata}

### 평균 비트율

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **API 키:**<br/>media.qoe.bitrate </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> **전송 시점:**<br/>닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:800-899년 </li><li> **설명:**<br/>평균 비트 전송률(kbps)입니다. 이 값은 100kbps 간격으로 사전 정의된 버킷입니다. 평균 비트율은 재생 기간과 관련하여 재생 세션 중에 발생한 모든 비트율 값의 가중 평균으로 계산됩니다.에서 보냅니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bitrateAverageBucket) </li> <li> ****<br/> 하트비트:(l:stream:bitrate) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>평균 비트율 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **데이터 피드:**<br/>videoqoebitrateaverageevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>bitrateAverageBucket) </li> </ul> |


### 시작 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.qoe.timeToStart </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:3만 </li><li> **QoSObject**<br/>를 통해 설정하지 않으면 이 값의 기본값은 0입니다. 이 값의 설정 단위는 밀리초입니다. 값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>timeToStart) </li> <li> ****<br/> 하트비트:(l:stream:startup_time) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>시작 시간 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>timeToStart) </li> <li> **데이터 피드:**<br/>videoqoetimetostartevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |


### FPS

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.qoe.framesPerSecond </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:24년 </li><li> **설명:**<br/>스트림 프레임 속도의 현재 값(초당 프레임 수)입니다.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> ****<br/> 하트비트:(l:stream:fps) </li> </ul> | <ul> <li> **사용 가능:**<br/>아니요 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/>N/A </li> <li> **컨텍스트 데이터:**<br/> </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> </li> </ul> |



### 드롭된 프레임

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>droppedFrames </li> <li> **API 키:**<br/>media.qoe.droppedFrames </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:3 </li><li> **설명:**<br/>드롭된 프레임 수(Int). 이 값은 재생 세션 중에 드롭된 모든 프레임의 합계로 계산됩니다. 이 값은 (l:stream:dropped_frames)의 마지막 값에서 가져옵니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>droppedFrameCount) </li> <li> ****<br/> 하트비트:(l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>삭제된 프레임 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>droppedFrameCount) </li> <li> **데이터 피드:**<br/>videoqoedroppedframecountevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>droppedFrameCount) </li> </ul> |



### 버퍼 이벤트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:2 </li><li> **설명:**<br/>버퍼 이벤트 수입니다. 이 지표는 재생 세션 중에 발생한 다른 버퍼 상태의 수로 계산됩니다. 플레이어가 다른 상태에서 버퍼 상태에 들어가는 횟수입니다(예: 재생 또는 일시 정지).  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bufferCount) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>버퍼 이벤트 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>bufferCount) </li> <li> **데이터 피드:**<br/>videoqoebuffercountevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### 총 버퍼 지속 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:** </li> <li> ****<br/> 샘플 값:30년 </li><li> **설명:**<br/>버퍼링을 보낸 총 시간(초)입니다. 이 값은 재생 세션 중에 발생한 모든 버퍼 이벤트 기간의 합계로 계산됩니다. 값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다. <br/>**릴리스 날짜: 2018년 9월 13일**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bufferTime) </li> <li> ****<br/> 하트비트:(l:event:duration) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>총 버퍼 지속 시간 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>bufferTime) </li> <li> **데이터 피드:**<br/>videoqoebuffertimeevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



### 비트율 변경

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.qoe.bitrateChange </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:3 </li><li> **설명:**<br/>비트 전송률 변경 수(정수). 이 값은 재생 세션 중에 발생한 모든 비트율 변경 이벤트의 합계로 계산됩니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bitrateChangeCount) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>비트율 변경 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>bitrateChangeCount) </li> <li> **데이터 피드:**<br/>videoqoebitratechangecountevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### 오류/오류 이벤트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/> </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:1 </li><li> **설명:**<br/>발생한 오류 수(정수). 이 값은 재생 세션 중에 발생한 모든 오류 이벤트의 합계로 계산됩니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>errorCount) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=error) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>오류 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>errorCount) </li> <li> **데이터 피드:**<br/>videoqoeerrorcountevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



### 플레이어 SDK 오류 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/> </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>플레이어 SDK에서 생성된 고유한 오류 ID입니다. 고객은 제공된 오류 API를 통해 구현 시 오류 코드/ID를 제공해야 합니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>playerSdkErrors) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=error) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>오류 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>playerSdkErrors) </li> <li> ****<br/> 데이터 피드:videoqoeplayersdkerrors </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>playerSdkErrors) </li> </ul> |



### 외부 오류 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/> </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>외부 소스의 고유 오류 ID(예: CDN 오류)입니다. 고객은 제공된 오류 API를 통해 구현 시 오류 코드/ID를 제공해야 합니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>externalErrors) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=error) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>오류 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>externalErrors) </li> <li> ****<br/> 데이터 피드:videoqoeextenerrors </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>externalErrors) </li> </ul> |



### Media SDK 오류 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/> </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>재생 중 Media SDK에서 생성된 고유한 오류 ID입니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>mediaSdkErrors) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=error) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>오류 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>mediaSdkErrors) </li> <li> **데이터 피드:** <br/>mediaqoeexternalerrors </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>mediaSdkErrors) </li> </ul> |




### 세션 종료 {#session-end}

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/> </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:** 2.1 </li> <li> ****<br/> 샘플 값:end </li><li> **설명:**<br/>최종 이벤트는 SDK가 백 엔드에 대한 닫기 호출을 전송함을 의미합니다. 이 이벤트를 수신하면 백엔드가 이 비디오에 대한 세션을 닫고 추가 처리를 수행하지 않습니다. <br/>미디어가 100%로 완료된 경우 관련 정보는 컨텐츠 `s:event:type=complete.` 완료 [참조 후](audio-video-parameters.md#content-complete) 전송해야 합니다. </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> ****<br/> 하트비트:(s:event:type=end) </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>N/A </li> <li> **컨텍스트 데이터:**<br/> </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> </li> </ul> |



## 품질 지표 {#quality-metrics}

### 시작 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:3만 </li><li> **QoSObject**<br/>를 통해 설정하지 않으면 이 값의 기본값은 0입니다. 이 값의 설정 단위는 밀리초입니다. 값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다. <br/>**릴리스 날짜: 2018년 9월 13일**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>timeToStart) </li> <li> ****<br/> 하트비트:(l:stream:startup_time) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>시작 시간 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>timeToStart) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |



### 버퍼 이벤트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:2 </li><li> **설명:**<br/>버퍼 이벤트(정수) 수입니다. 이 지표는 재생 세션 중에 발생한 버퍼 이벤트 수로 계산됩니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bufferCount) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>버퍼 이벤트 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>bufferCount) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### 총 버퍼 지속 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:15년 </li><li> **설명:**<br/>버퍼링 총 시간(초;정수). 이 값은 재생 세션 중에 발생한 모든 버퍼 이벤트 기간의 합계로 계산됩니다. 값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다. <br/>**릴리스 날짜: 2018년 9월 13일**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bufferTime) </li> <li> ****<br/> 하트비트:(l:event:duration) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>총 버퍼 지속 시간 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>bufferTime) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



### 비트율 변경

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>이벤트 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:"3" </li><li> **설명:**<br/>비트 전송률 변경 횟수입니다. 이 값은 재생 세션 중에 발생한 모든 비트율 변경 이벤트의 합계로 계산됩니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bitrateChangeCount) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>비트율 변경 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>bitrateChangeCount) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### 오류

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:1 </li><li> **설명:**<br/>발생한 오류 수(정수). 이 값은 재생 세션 중에 발생한 모든 오류 이벤트의 합계로 계산됩니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>errorCount) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=error) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>오류 이벤트 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>errorCount) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



### 드롭된 프레임

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:1 </li><li> **설명:**<br/>드롭된 프레임 수(정수). 이 값은 재생 세션 중에 드롭된 모든 프레임의 합계로 계산됩니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>droppedFrameCount) </li> <li> ****<br/> 하트비트:(l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>삭제된 프레임 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>droppedFrameCount) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>droppedFrameCount) </li> </ul> |



### 시작 전 드롭

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:TRUE </li><li> **설명:**<br/>사용자가 비디오를 시작하기 전에 비디오를 종료한 횟수입니다. 이 지표는 광고에 관계없이 컨텐츠가 렌더링되지 않은 경우에만 1로 설정됩니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>dropBeforeStart) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=aa_start) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>시작 전 드롭 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>dropBeforeStart) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>dropBeforeStart) </li> </ul> |



>[!IMPORTANT]
>이 이벤트가 설정되면 가능한 값은 TRUE뿐입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.

### 버퍼 영향을 받은 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:TRUE </li><li> **설명:**<br/>버퍼링에 의해 영향을 받는 스트림 수입니다. 이 지표는 재생 세션 중에 하나 이상의 버퍼 이벤트가 발생한 경우에만 1로 설정됩니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>buffer) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>버퍼 영향을 받은 스트림 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>buffer) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>이 이벤트가 설정되면 가능한 값은 TRUE뿐입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.

### 비트율 변경의 영향을 받은 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:TRUE </li><li> **설명:**<br/>비트율 변경이 발생한 스트림의 수입니다. 이 지표는 재생 세션 중에 하나 이상의 비트율 변경 이벤트가 발생한 경우에만 1로 설정됩니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bitrateChange) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> ****<br/> 보고서 이름:비트율 변경 영향을 받은 스트림 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>bitrateChange) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>bitrateChange) </li> </ul> |



>[!IMPORTANT]
>이 이벤트가 설정되면 가능한 값은 TRUE뿐입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.

### 평균 비트율

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:3200년 </li><li> **설명:**<br/>평균 비트 전송률(kbps, 정수)입니다. 이 지표는 재생 기간과 관련하여 재생 세션 중에 발생한 모든 비트율 값의 가중 평균으로 계산됩니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bitrateAverage) </li> <li> ****<br/> 하트비트:(l:stream:bitrate) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>평균 비트율 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>bitrateAverage) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>bitrateAverage) </li> </ul> |



### 오류 영향을 받은 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:TRUE </li><li> **설명:**<br/>오류 이벤트가 발생한 스트림 수(즉, 재생 세션 중에 호출되었고 `trackError` `type=error` 하트비트 호출이 생성됨)입니다. </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>라는 오류가 표시됩니다) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=error) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>오류 영향을 받은 스트림 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>라는 오류가 표시됩니다) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>라는 오류가 표시됩니다) </li> </ul> |



>[!IMPORTANT]
>이 이벤트가 설정되면 가능한 값은 TRUE뿐입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.

### 드롭된 프레임 영향을 받은 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:TRUE </li><li> **설명:**<br/>프레임을 삭제한 스트림의 수입니다. 이 지표는 재생 세션 중에 하나 이상의 프레임이 드롭된 경우에만 1로 설정됩니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>droppedFrames) </li> <li> ****<br/> 하트비트:(l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>드롭된 프레임 영향을 받은 스트림 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>droppedFrames) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>droppedFrames) </li> </ul> |



>[!IMPORTANT]
>이 이벤트가 설정되면 가능한 값은 TRUE뿐입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.

### 지연 영향을 받은 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5+ </li> <li> ****<br/> 샘플 값:TRUE </li><li> **설명:**<br/>중단된 이벤트가 발생한 스트림의 수입니다. 이 지표는 재생 중에 하나 이상의 정지가 발생한 경우에만 1로 설정됩니다. 고객이 보고에 사용할 수 있는 값을 갖도록 고유한 처리 규칙을 만들어야 합니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>stall) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=stall) </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/> </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>stall) </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>stall) </li> </ul> |



>[!IMPORTANT]
>이 이벤트가 설정되면 가능한 값은 TRUE뿐입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.

### 지연 이벤트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5+ </li> <li> ****<br/> 샘플 값:"3" </li><li> **설명:**<br/>재생 세션 중에 재생이 중단된 횟수입니다. 고객이 보고에 사용할 수 있는 값을 갖도록 고유한 처리 규칙을 만들어야 합니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>stallCount) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=stall) </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/> </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>stallCount) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>stallCount) </li> </ul> |



### 총 지연 기간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5+ </li> <li> ****<br/> 샘플 값:12년 </li><li> **설명:**<br/>총 시간(초;integer) 재생 세션 중에 재생이 중단되었습니다. 고객이 보고에 사용할 수 있는 값을 갖도록 고유한 처리 규칙을 만들어야 합니다.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>stallTime) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=stall) </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/> </li> <li> ****<br/> 컨텍스트 데이터:(a.media.qoe.<br/>stallTime) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe.<br/>stallTime) </li> </ul> |



## 관련 API {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

