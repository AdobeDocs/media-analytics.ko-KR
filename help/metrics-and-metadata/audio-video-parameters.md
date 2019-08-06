---
seo-title: 오디오 및 비디오 매개 변수
title: 오디오 및 비디오 매개 변수
uuid: fdacfb 8 b-db 3 e -46 fb-b 9 ad-c 3 a 749555 b 2 a
translation-type: tm+mt
source-git-commit: a9e1c8ba7c8a95120e4c66460ff6d742c0855652

---


# 오디오 및 비디오 매개 변수{#audio-and-video-parameters}

>[!IMPORTANT]
>
>2019 년 2 월 7 일, 비디오 및 오디오용 Adobe Analytics에서 지표 이름이 변경되었습니다. <i>Media Initiates</i>의 이름이 <i>Media Starts</i>로 변경됩니다. 이러한 변경은 지표 및 보고에서 업계 표준을 반영하고 보고에서 지표를 쉽게 식별할 수 있도록 변경되었습니다.

>[!NOTE]
>
>2018 년 9 월 13 일부터 일부 차원, 지표 및 보고서에 대한 레이블이 변경되어 비디오 및 오디오 분석에 대한 컨텐츠 간 추적을 허용했습니다. 이러한 레이블로는 *비디오 시작*&#x200B;이 *미디어 시작*&#x200B;으로, *비디오 길이*&#x200B;가 *컨텐츠 길이*&#x200B;로, *비디오 이름*&#x200B;이 *컨텐츠 이름*&#x200B;으로 변경되었습니다. Reports &amp; Analytics의 비디오 보고서는 모두 이름을 "비디오"가 아닌 "미디어"를 사용하도록 업데이트되었습니다. 레이블 변경으로 데이터 수집 또는 히스토리 데이터가 변경되지는 않았습니다. Report Builder나 이러한 변경의 영향을 받을 수 있는 다른 외부의 자동화된 데이터 가져오기에서 이러한 레이블을 사용하는 경우에 대비해 이러한 변경 내용을 적어 두십시오.

이 항목에서는 컨텍스트 데이터 값을 포함하여 Adobe에서 솔루션 변수를 통해 수집하는 오디오 및 비디오 컨텐츠 데이터의 목록을 제공합니다.

테이블 데이터 설명:

* **구현:**&#x200B;구현 값 및 요구 사항에 대한 정보
   * *키* - 앱에서 수동으로 설정하거나 Adobe Media SDK에 의해 자동으로 설정된 변수.
   * *필수* - 기본 오디오 및 비디오 추적에 매개 변수가 필요한지 여부를 나타냅니다.
   * *유형* - 설정할 변수의 유형(문자열 또는 숫자)을 지정합니다.
   * *보낸 날짜* - 데이터가 전송되는 시기를 나타냅니다. *미디어 시작은* 미디어 시작 시 전송된 분석 호출이고 *, 광고 시작은* 광고 시작 시 전송된 분석 호출입니다. *닫기* 호출은 하트비트 서버에서 미디어 세션이 끝날 때 Analytics 서버로 바로 전송되는 컴파일된 Analytics 호출이나 광고, 장 (chapter) 의 끝입니다. 네트워크 패킷 호출에서는 Close 호출을 사용할 수 없습니다.
   * *최소. SDK 버전* - 매개 변수에 액세스하는 데 필요한 SDK 버전을 나타냅니다.
   * *샘플 값* - 일반 변수 사용법 예를 제공합니다.
* **네트워크 매개 변수:** Adobe Analytics 또는 하트비트 서버에 전달되는 값을 표시합니다. 이 열에는 Adobe Media SDK에서 생성한 네트워크 호출에 표시되는 매개 변수의 이름이 표시됩니다.
* **보고:** 오디오 및 비디오 데이터를 보고 분석하는 방법에 대한 정보입니다.
   * *사용 가능* - 기본적으로 데이터를 보고할 수 있는지(*Yes*) 또는 사용자 지정 설정(*Custom*)이 필요한지 여부를 나타냅니다.
   * *예약된 변수* - 데이터가 예약된 변수의 이벤트, eVar, prop 또는 분류로 캡처되는지 여부를 나타냅니다.
   * *만료* - 각 히트 후에 또는 방문 후에 데이터가 만료되는지 여부를 나타냅니다.
   * *보고서 이름* - 변수에 대한 Adobe Aanlytics 보고서 이름
   * *컨텍스트 데이터* - 보고 서버에 전달되고 처리 규칙에 사용되는 Adobe Analytics 컨텍스트 데이터의 이름.
   * *데이터 피드* - 클릭스트림 또는 라이브 스트림 데이터 피드에서 찾은 변수의 열 이름
   * *Audience Manager* - Adobe Audience Manager에 있는 Trait 이름

>[!IMPORTANT]
>
>아래에 나열된 변수에 대한 분류 이름은 보고/예약 변수 아래에 "분류" 로 설명하지 마십시오.\
>미디어 분류는 미디어 추적에 대해 보고서 세트가 활성화되어 있을 때 정의됩니다. Adobe는 때때로 새 속성을 추가하며, 이러한 경우 고객은 보고서 세트를 다시 활성화하여 새 미디어 속성에 액세스해야 합니다. 업데이트 프로세스 동안 Adobe는 변수의 이름을 검사하여 분류를 사용할지 여부를 결정합니다. 누락된 경우 누락된 항목이 추가됩니다.

## 코어 오디오 및 비디오 데이터 {#section_y55_y1m_n1b}

### 스트림 유형 {#stream-type}

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.streamType </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 2.2 <br/><br/>[Media Collection API 개요](/help/media-collection-api/mc-api-overview.md) 또는 SDK [다운로드 - 버전 2.2에서 사용할 수 있습니다](/help/sdk-implement/download-sdks.md).  </li>  <li> **샘플 값:** <br/>"video" </li> <li> **설명:**<br/> 스트림 유형을 식별합니다. 유효한 값은 "audio", "video", ""입니다.  <br/><br/>[보고 세그먼트](/help/metrics-and-metadata/segments.md): <br/><br/>미디어 스트림 유형: 모두 - <br/>모든 미디어 스트림 데이터를 세그먼트화합니다. 규칙: 컨텐츠 (ID) 가 <br/><br/>미디어 스트림 유형을 포함함: 오디오 - <br/>모든 오디오 스트림 데이터 세그먼트 규칙: 컨텐츠 (id) 가 존재하며 미디어 스트림 유형 = audio <br/><br/>media stream type: " video " - <br/>모든 비디오 스트림 데이터 세그먼트 규칙: 컨텐츠 (ID) 가 존재하며 미디어 스트림 유형이 있습니다!= audio <br/><br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. streamtype) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. streamtype) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>방문 시 </li> <li> **보고서 이름:**<br/>컨텐츠 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. streamtype) </li> <li> **데이터 피드:** <br/>videostreamtype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### 컨텐츠 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.id </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>"4586695ABC" </li> <li>**설명:**<br/> 컨텐츠의 컨텐츠 ID를 참조하십시오. 이 ID 는 `s:asset:video_id.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. name) </li> <li> **하트 비트:**<br/> (s: 자산: video_ id) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>방문 시 </li> <li> **보고서 이름:**<br/>컨텐츠 </li> <li> **컨텍스트 데이터:**<br/> (a. media. name) </li> <li> **데이터 피드:**<br/>비디오 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 컨텐츠 길이(변수)

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.length </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> VOD: 128; 라이브: 86400; 선형: 1800. </li><li> **설명:**<br/> 클립 길이/런타임 - 소비되는 컨텐츠의 최대 길이 (또는 지속 시간) 입니다 (초). It equals the last value of `l:asset:length` from events of type Main. <br/>가 `l:asset:length` 설정되지 않은 경우의 `l:asset:duration` 마지막 값이 사용됩니다. <br/>보고에서 "비디오 길이"는 분류이고 "컨텐츠 길이(변수)"는 eVAR입니다.  <br/> **중요:** 이 속성은 진행 추적 지표 및 대상 평균 시간과 같은 여러 지표를 계산하는 데 사용됩니다. 이 값이 설정되지 않았거나 0보다 크지 않으면 이러한 지표를 사용할 수 없습니다.  알 수 없는 기간이 있는 라이브 미디어의 경우 기본값은 86400입니다. <br/>이전 버전 1.5.1, this was `l:asset:duration`; 1.5.1 이후로는 `l:asset:length.`<br/> **릴리스 날짜: 2018년 9월 13일** </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. length) </li> <li> **하트 비트:**<br/> (L: 자산: 길이) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> 컨텐츠 길이(변수) </li> <li> **컨텍스트 데이터:**<br/> (a. media. length) </li> <li> **데이터 피드:**<br/>videolength </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 비디오 길이

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.length </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> VOD: 128; 라이브: 86400; 선형: 1800. </li> <li> **설명:**<br/> 클립 길이/런타임 - 소비되는 컨텐츠의 최대 길이 (또는 지속 시간) 입니다 (초). It equals the last value of `l:asset:length` from events of type Main. If `l:asset:length` is not set, then the last value of `l:asset:duration` is used. 보고에서 "비디오 길이"는 분류이고 "컨텐츠 길이(변수)"는 eVAR입니다.  <br/> **중요:** 이 속성은 진행 추적 지표 및 대상 평균 시간과 같은 여러 지표를 계산하는 데 사용됩니다. 이 값이 설정되지 않았거나 0보다 크지 않으면 이러한 지표를 사용할 수 없습니다.  알 수 없는 기간이 있는 라이브 미디어의 경우 기본값은 86400입니다. Pre Version 1.5.1, this was `l:asset:duration`; after 1.5.1, this is `l:asset:length.`<br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. length) </li> <li> **하트 비트:**<br/> (L: 자산: 길이) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> 비디오 길이 </li> <li> **컨텍스트 데이터:**<br/> (a. media. length) </li> <li> **데이터 피드:** <br/>videoclassificationlength </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 컨텐츠 유형

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.contentType </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>제한된 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>"vod" </li> <li> **설명:**<br/> 스트림 유형당 **사용 가능한 값**: <br/> _오디오:_ "song", "podcast", "audiobook", "radio" <br/> _비디오:_ " vod "," live "," linear "," ugc "," dvod " <br/> 고객은 이 매개 변수에 대한 사용자 지정 값을 제공할 수 있습니다. 이것은 설정이 해제된 `s:stream:type.` 경우 같음 `missing_content_type.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. contenttype) </li> <li> **하트 비트:**<br/> (s: 스트림: 유형) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>컨텐츠 유형 </li> <li> **컨텍스트 데이터:**<br/> (a. contenttype) </li> <li> **데이터 피드:**<br/>videocontenttype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### 미디어 세션 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>백엔드에서 가져옴 </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.8 </li> <li> **샘플 값:**<br/>1482236761294786918253 </li> <li> **설명:**<br/> 이것은 개별 재생에 고유한 컨텐츠 스트림의 인스턴스를 식별합니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. vsid) </li> <li> **하트비트:**<br/> (s: 이벤트: sid) </li> </ul> | <ul> <li> **사용 가능:**<br/>처리 규칙 사용 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/>사용자 지정 </li> <li> **컨텍스트 데이터:**<br/> (a. media. vsid) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.vsid) </li> </ul> |

### 컨텐츠 플레이어 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **API 키:**<br/>media.playerName </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> " brightcove " </li> <li> **설명:**<br/> 플레이어의 이름입니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>playerName) </li> <li> **하트 비트:**<br/> (s: SP: player_ name) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>컨텐츠 플레이어 이름 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. playername) </li> <li> **데이터 피드:**<br/>videoplayername </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.playerName) </li> </ul> |

### 컨텐츠 채널

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **API 키:**<br/>media.channel </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>"Sports" </li> <li> **설명:**<br/> 배포 스테이션/채널 또는 컨텐츠가 재생되는 위치. 여기에 모든 문자열 값이 허용됩니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. channel) </li> <li> **하트 비트:**<br/> (s: SP: 채널) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>컨텐츠 채널 </li> <li> **컨텍스트 데이터:**<br/> (a. media. channel) </li> <li> **데이터 피드:**<br/>videochannel </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.channel) </li> </ul> |

### 컨텐츠 세그먼트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> " 0-10 " </li> <li> **설명:**<br/> 본 컨텐츠의 일부 (분 단위) 를 설명하는 간격입니다. 세그먼트는 재생 세션 중 최대 및 최소 플레이헤드 값으로 계산됩니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>컨텐츠 세그먼트 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. segment) </li> <li> **데이터 피드:**<br/>videosegment </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.segment) </li> </ul> |

### 컨텐츠 이름(변수)

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [이름](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.name </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.1 </li> <li> **샘플 값:**<br/>"The Big Bang Theory" </li> <li> **설명:**<br/>이것은 컨텐츠의 "친숙한" (사람이 읽을 수 있는) 이름이며 `s:asset:name.`<br/>, 이것은 보고의 마지막 값과 동일하고, 비디오 이름은 분류이고, 컨텐츠 이름 (변수) 는 Evar 입니다. <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>friendlyname) </li> <li> **하트 비트:**<br/> (s: 자산: 이름) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> 컨텐츠 이름(변수) </li> <li> **컨텍스트 데이터:**<br/> (a. media. friendlyname) </li> <li> **데이터 피드:**<br/>videoname </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 비디오 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [이름](./audio-video-parameters.md#config-media-object) </li> <li> **API 키:**<br/>media.name </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.1 </li> <li> **샘플 값:**<br/>"The Big Bang Theory" </li> <li> **설명:**<br/> 이것은 컨텐츠의 "친숙한" (사람이 읽을 수 있는) 이름이며 `s:asset:name.`<br/>, 이것은 보고의 마지막 값과 동일하고, 비디오 이름은 분류이고, 컨텐츠 이름 (변수) 는 Evar 입니다. <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>friendlyname) </li> <li> **하트 비트:**<br/> (s: 자산: 이름) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> 비디오 이름 </li> <li> **컨텍스트 데이터:**<br/> (a. media. friendlyname) </li> <li> **데이터 피드:** <br/>videoclassificationname </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.friendlyName) </li> </ul> |

### 비디오 경로

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>"4586695ABC" </li> <li> **설명:**<br/> 사이트 및/또는 앱에서 뷰어 경로를 추적하여 특정 비디오를 보는 데 사용한 경로를 확인할 수 있습니다. 모든 정수 및/또는 문자 조합입니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. name) </li> <li> **하트 비트:**<br/> (s: 자산: video_ id) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>prop </li> <li> **보고서 이름:**<br/>비디오 경로 </li> <li> **컨텍스트 데이터:**<br/> (a. media. name) </li> <li> **데이터 피드:**<br/>videopath </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.name) </li> </ul> |

### SDK 버전

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **API 키:**<br/>media.sdkVersion </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>"2.62.0_release" </li> <li> **설명:**<br/> 플레이어에서 사용하는 SDK 버전. 플레이어에 적합한 사용자 지정 값을 가질 수 있습니다. <br/><br/>고객이 보고에 사용할 수 있는 값을 갖도록 고유한 처리 규칙을 만들어야 합니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Sdkversion) </li> <li> **하트 비트:**<br/> (s: SP: sdk) </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/> </li> <li> **컨텍스트 데이터:**<br/> (a. media. sdkversion) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### VHL 버전

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>"js-2.0.1.88-c8c0b1" </li> <li> **설명:**<br/> 추적 세션에 사용되는 Media SDK 버전. <br/><br/>고객이 보고에 사용할 수 있는 값을 갖도록 고유한 처리 규칙을 만들어야 합니다.  <br/><br/>[Mediaheartbeat. version ();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Vhlversion) </li> <li> **하트 비트:**<br/> (s: SP: hb_ version) </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/>사용자 지정 </li> <li> **컨텍스트 데이터:**<br/> (a. media. vhlversion) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## 표준 오디오 및 비디오 메타데이터 {#section_pfc_hbm_n1b}

### 표시

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>SHOW </li> <li> **API 키:**<br/>media.show </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> " 모던한 가족 "" 블랙리스트 "" 새로운 소녀 " </li> <li> **설명:**<br/> 프로그램/시리즈 이름 <br/>프로그램 이름은 해당 프로그램이 시리즈에 속한 경우에만 필요합니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. show) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. show) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>표시 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. show) </li> <li> **데이터 피드:**<br/>videoshow </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.show) </li> </ul> |

### 스트림 형식

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>STREAM_FORMAT </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>"Live" </li> <li> **설명:**<br/> 스트림의 형식 (라이브, VOD, 리니어) 입니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. format) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. format) </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/>사용자 지정 </li> <li> **컨텍스트 데이터:**<br/> (a. media. format) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.format) </li> </ul> |

### 시즌

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>SEASON </li> <li> **API 키:**<br/>media.season </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>"2" </li> <li> **설명:**<br/> 쇼가 속하는 계절 번호입니다. 시즌 시리즈는 쇼가 시리즈인 경우에만 필요합니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. season) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. season) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>시즌 </li> <li> **컨텍스트 데이터:**<br/> (a. media. season) </li> <li> **데이터 피드:**<br/>videoseason </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.season) </li> </ul> |

### 에피소드

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>EPISODE </li> <li> **API 키:**<br/>media.episode </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>"13" </li> <li> **설명:**<br/> 에피소드 수입니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. 에피소드) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. 에피소드) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>에피소드 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. 에피소드) </li> <li> **데이터 피드:**<br/>videoepisode </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.episode) </li> </ul> |

### 자산 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>ASSET_ID </li> <li> **API 키:**<br/>media.assetId </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>"89745363" </li> <li> **설명:**<br/> TV 시리즈 에피소드 식별자, 동영상 자산 식별자 또는 라이브 이벤트 식별자와 같은 미디어 자산의 고유한 식별자입니다. 일반적으로 이러한 ID는 EIDR, TMS/Gracenote 또는 Rovi와 같은 메타데이터 권한에서 파생됩니다. 이러한 식별자는 다른 소유 시스템이나 사내 시스템에서 파생될 수도 있습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. asset) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. asset) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/> 자산 ID </li> <li> **컨텍스트 데이터:**<br/> (a. Media. asset) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.asset) </li> </ul> |

### 장르

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>GENRE </li> <li> **API 키:**<br/>media.genre </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> " drama "," comedy " </li> <li> **설명:**<br/> 컨텐츠 프로듀서에 의해 정의된 컨텐츠의 유형 또는 그룹입니다. 값은 변수 구현에서 쉼표로 구분해야 합니다. 보고에서 List eVar는 각 라인 항목이 동일한 지표 가중치를 받는 라인 항목으로 각 값을 나눕니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. genre) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. genre) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>List eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>장르 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. genre) </li> <li> **데이터 피드:**<br/>videogenre </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.genre) </li> </ul> |

### 최초 방송 날짜

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>FIRST_AIR_DATE </li> <li> **API 키:**<br/>media.firstAirDate </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> " 2016-01-25 " </li> <li> **설명:**<br/> 컨텐츠가 TV에서 처음 방송되는 날짜입니다. 모든 날짜 형식이 허용되지만, Adobe는 YYYY-MM-DD 형식을 권장합니다. </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. airdate) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. airdate) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> 최초 방송 날짜 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. airdate) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.airDate) </li> </ul> |

### 최초 디지털 날짜

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>FIRST_DIGITAL_DATE </li> <li> **API 키:**<br/>media.firstDigitalDate </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> " 2016-01-25 " </li> <li> **설명:**<br/> 컨텐츠가 디지털 채널 또는 플랫폼에서 처음 방송된 날짜입니다. 모든 날짜 형식이 허용되지만, Adobe는 YYYY-MM-DD 형식을 권장합니다. </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. digitaldate) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. digitaldate) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/> 최초 디지털 날짜 </li> <li> **컨텍스트 데이터:**<br/> (a. media. digitaldate) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.digitalDate) </li> </ul> |

### 컨텐츠 등급

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>RATING </li> <li> **API 키:**<br/>media.rating </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> Tvy, TVG, TVPG, TVMA </li> <li> **설명:**<br/> TV 부모의 지침에 따라 정의된 등급입니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. rating) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. ratings) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/> 컨텐츠 등급 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. rating) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.rating) </li> </ul> |

### 작성자

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>ORIGINATOR </li> <li> **API 키:**<br/>media.originator </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> " Warner Brothers "," Sony "," Disney " </li> <li> **설명:**<br/> 컨텐츠 작성자입니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. originator) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. originator) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/> 작성자 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. originator) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.originator) </li> </ul> |

### 네트워크

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>NETWORK </li> <li> **API 키:**<br/>media.network </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> " fox "," bravo "," espn " </li> <li> **설명:**<br/> 네트워크/채널 이름.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. network) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. network) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>네트워크 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. network) </li> <li> **데이터 피드:**<br/>videonetwork </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.network) </li> </ul> |

### 표시 유형

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>SHOW_TYPE </li> <li> **API 키:**<br/>media.showType </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> " 0 " = 전체 에피소드; " 1 " = 미리 보기/트레일러; " 2 " = clip; " 3 " = other. </li> <li> **설명:**<br/> 컨텐츠 유형 - 0와 3 사이의 정수로 표현됩니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. type) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. type) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>표시 유형 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. type) </li> <li> **데이터 피드:**<br/>videoshowtype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>MVPD </li> <li> **API 키:**<br/>media.pass.mvpd </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> " comcast "," directv "," dish " </li> <li> **설명:**<br/> MVPD는 Adobe 인증을 통해 제공됩니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. pass. mvpd) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. Pass.<br/>mvpd) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>MVPD </li> <li> **컨텍스트 데이터:**<br/> (a. media. pass. mvpd) </li> <li> **데이터 피드:**<br/>videomvpd </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### 인증됨

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>AUTHORIZED </li> <li> **API 키:**<br/>media.pass.auth </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> " true " </li> <li> **설명:**<br/> 사용자가 Adobe 인증을 통해 인증되었습니다. <br/>**중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. Pass. auth) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. Pass.<br/>auth) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>인증됨 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. Pass. auth) </li> <li> **데이터 피드:**<br/>videoauthorized </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pass.auth) </li> </ul> |

### 방송 시간대

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>DAY_PART </li> <li> **API 키:**<br/>media.dayPart </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> </li> <li> **설명:**<br/> 컨텐츠가 방송되거나 재생되는 시간을 정의하는 속성입니다. 이는 고객이 필요에 따라 모든 값을 설정할 수 있습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. daypart) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. daypart) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>방송 시간대 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. daypart) </li> <li> **데이터 피드:**<br/>videodaypart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.dayPart) </li> </ul> |

### 미디어 피드 유형

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>FEED </li> <li> **API 키:**<br/>media.feed </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> " east-hd "," west-hd "," east-sd " </li> <li> **설명:**<br/> 피드 유형. <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. feed) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. feed) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> 미디어 피드 유형 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. feed) </li> <li> **데이터 피드:**<br/>videofeedtype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.feed) </li> </ul> |

### 아티스트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.artist </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 <br/>[미디어 컬렉션 개요](/help/media-collection-api/mc-api-overview.md) 또는 [SDK 다운로드 - 버전 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **샘플 값:** <br/>"The Beatles" </li> <li> **설명:**<br/> 아티스트의 이름입니다. <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. artist) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. artist) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> </li> <li> **컨텍스트 데이터:**<br/> (a. Media. artist) </li> <li> **데이터 피드:** <br/>videoaudioartist </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.artist) </li> </ul> |

### 앨범

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.album </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 <br/>[미디어 컬렉션 개요](/help/media-collection-api/mc-api-overview.md) 또는 [SDK 다운로드 - 버전 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **샘플 값:**<br/>"Revolver" </li> <li> **설명:**<br/> 앨범의 이름입니다. <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. album) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. album) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> </li> <li> **컨텍스트 데이터:**<br/> (a. Media. album) </li> <li> **데이터 피드:** <br/>videoaudioalbum </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.album) </li> </ul> |

### 레이블

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.label </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 <br/>[미디어 컬렉션 개요](/help/media-collection-api/mc-api-overview.md) 또는 [SDK 다운로드 - 버전 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **샘플 값:**<br/>"Revolver" </li> <li> **설명:**<br/> 레코드 레이블의 이름입니다. <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. label) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. label) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> </li> <li> **컨텍스트 데이터:**<br/> (a. media. label) </li> <li> **데이터 피드:** <br/>videoaudiolabel </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.label) </li> </ul> |

### Author

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.author </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 <br/>[미디어 컬렉션 개요](/help/media-collection-api/mc-api-overview.md) 또는 [SDK 다운로드 - 버전 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **샘플 값:** <br/>"John Kennedy Toole" </li> <li> **설명:**<br/> Audiobook의 작성자 이름입니다. <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. author) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. author) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> </li> <li> **컨텍스트 데이터:**<br/> (a. Media. author) </li> <li> **데이터 피드:** <br/>videoaudioauthor </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.author) </li> </ul> |

### 방송국

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.station </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 <br/>[미디어 컬렉션 개요](/help/media-collection-api/mc-api-overview.md) 또는 [SDK 다운로드 - 버전 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **샘플 값:** <br/>"NPR" </li> <li> **설명:**<br/> 라디오 방송국 이름/ID. <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. station) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. station) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> </li> <li> **컨텍스트 데이터:**<br/> (a. Media. station) </li> <li> **데이터 피드:**<br/>videoaudiostation </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.station) </li> </ul> |

### 게시자

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.publisher </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 <br/>[미디어 컬렉션 개요](/help/media-collection-api/mc-api-overview.md) 또는 [SDK 다운로드 - 버전 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **샘플 값:** <br/>"Random Bauhaus" </li> <li> **설명:**<br/> 오디오 콘텐트 게시자의 이름입니다. <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. publisher) </li> <li> **하트 비트:**<br/> (s: META:<br/>a. Media. publisher) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> </li> <li> **컨텍스트 데이터:**<br/> (a. Media. publisher) </li> <li> **데이터 피드:**<br/>videoaudiopublisher </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.publisher) </li> </ul> |

## 오디오 및 비디오 지표 {#section_3D5F9C555274428AA6030D07596177E9}

### 미디어 시작

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/> 문자열</li> <li> **보낸 사람:**<br/> 미디어 시작</li> <li> **최소. SDK 버전:**&#x200B;모두</li> <li> **샘플 값:**<br/>TRUE </li> <li> **설명:**<br/> 미디어에 대한 load event. 이 이벤트는 뷰어가 _재생_ 단추를 클릭할 때 발생합니다. 이 이벤트는 프리롤 광고, 버퍼링, 오류 등이 있는 경우에도 계산됩니다.  <br/>**중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. view) </li> <li> **하트 비트:**<br/> (s: 이벤트:<br/>type = start) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/> 미디어 시작 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. view) </li> <li> **데이터 피드:**<br/>videostart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.view) </li> </ul> |

### 컨텐츠 시작

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>TRUE </li> <li> **설명:**<br/> 미디어의 첫 번째 프레임이 소비됩니다. 광고, 버퍼링 중에 사용자가 그만두면 "컨텐츠 시작" 이벤트가 일어나지 않습니다.  <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>컨텐츠 시작 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. play) </li> <li> **데이터 피드:**<br/>videoplay </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.play) </li> </ul> |

### 컨텐츠 완료 {#content-complete}

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>TRUE </li> <li> **설명:**<br/> 완료까지 본 스트림. 이는 사용자가 전체 스트림을 시청했거나 듣지 않아도 됩니다. 이전에 건너뛸 수도 있었지만 이는 사용자가 스트림의 끝에 도달했음을 의미합니다. <br/>[세션 끝 참조](quality-parameters.md#session-end)<br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트 비트:**<br/> (s: 이벤트:<br/>type = complete) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>컨텐츠 완료 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. complete) </li> <li> **데이터 피드:**<br/>videocomplete </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.complete) </li> </ul> |

### 컨텐츠 체류 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>105 </li> <li> **설명:**<br/> 기본 컨텐츠에서 play 유형의 모든 이벤트에 대한 이벤트 기간 (초) 를 계산합니다. 값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다.  <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>컨텐츠 체류 시간 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. timeplayed) </li> <li> **데이터 피드:**<br/>videotime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.timePlayed) </li> </ul> |

### 미디어 사용 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>120 </li> <li> **설명:**<br/> 기본 및 광고 컨텐츠 둘 다 play 유형의 모든 이벤트에 대한 이벤트 기간 (초) 를 계산합니다. 값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다.  <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/> 미디어 사용 시간 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. totaltimeplay) </li> <li> **데이터 피드:**<br/>videototaltime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### 재생된 고유 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>94 </li> <li> **설명:**<br/> 세션 중에 재생되는 컨텐츠의 고유한 세그먼트 값 (초) 입니다. 시청자가 컨텐츠에서 동일한 세그먼트를 여러 번 본다는 다시 찾기 시나리오에서 재생되는 시간은 제외합니다.  값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다.  <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>사용자 지정 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. uniquetimeplay) </li> <li> **데이터 피드:**<br/>videouniquetimeplayed </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. uniquetimeplayed) </li> </ul> |

### 10 % 진행률 마커

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>TRUE </li> <li> **설명:**<br/> 재생 헤드는 길이에 따라 컨텐츠의 10% 마커를 전달합니다. 마커는 역방향을 찾으려는 경우에도 한 번만 계산됩니다. 정방향으로 찾는 경우 건너뛴 마커는 계산되지 않습니다.  <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>10% 진행률 마커 </li> <li> **컨텍스트 데이터:**<br/> (a. media. progress 10) </li> <li> **데이터 피드:**<br/>videoprogress10 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress10) </li> </ul> |

### 25 % 진행률 마커

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>TRUE </li> <li> **설명:**<br/> 재생 헤드는 컨텐츠 길이에 따라 컨텐츠의 25% 마커를 전달합니다. 마커는 역방향을 찾으려는 경우에도 한 번만 계산됩니다. 정방향으로 찾는 경우 건너뛴 마커는 계산되지 않습니다.  <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>25% 진행률 마커 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. progress 25) </li> <li> **데이터 피드:**<br/>videoprogress25 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress25) </li> </ul> |

### 5% 진행률 마커

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>TRUE </li> <li> **설명:**<br/> 재생 헤드는 컨텐츠 길이에 따라 컨텐츠의 50% 마커를 전달합니다. 마커는 역방향을 찾으려는 경우에도 한 번만 계산됩니다. 정방향으로 찾는 경우 건너뛴 마커는 계산되지 않습니다.  <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>50% 진행률 마커 </li> <li> **컨텍스트 데이터:**<br/> (a. media. progress 50) </li> <li> **데이터 피드:**<br/>videoprogress50 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress50) </li> </ul> |

### 75% 진행률 마커

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/> **N/A** </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>TRUE </li> <li> **설명:**<br/> 재생 헤드는 컨텐츠 길이에 따라 컨텐츠의 75% 마커를 전달합니다. 마커는 역방향을 찾으려는 경우에도 한 번만 계산됩니다. 정방향으로 찾는 경우 건너뛴 마커는 계산되지 않습니다.  <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>75% 진행률 마커 </li> <li> **컨텍스트 데이터:**<br/> (a. media. progress 75) </li> <li> **데이터 피드:**<br/>videoprogress75 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress75) </li> </ul> |

### 95 % 진행률 마커

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>TRUE </li> <li> **설명:**<br/> 재생 헤드는 컨텐츠 길이에 따라 컨텐츠의 95% 마커를 전달합니다. 마커는 역방향을 찾으려는 경우에도 한 번만 계산됩니다. 정방향으로 찾는 경우 건너뛴 마커는 계산되지 않습니다.  <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>95% 진행률 마커 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. progress 95) </li> <li> **데이터 피드:**<br/>videoprogress95 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress95) </li> </ul> |

### Average Minute Audience

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>1보다 크거나 같음 </li> <li> **설명:**<br/> 평균 분 대상 지표는 특정 미디어 항목을 모든 재생 세션의 길이로 나눈 총 컨텐츠 체류 시간 (체류 시간) 로 계산됩니다. <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>대상 평균 시간(분) </li> <li> **컨텍스트 데이터:**<br/> (a. Media. averageminuteaudience) </li> <li> **데이터 피드:**<br/>videoaverageminuteaudience </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### 예상 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 1 - 19 분 재생 <br/>2 - 31 분 재생 <br/>3 - 78 분 재생 </li> <li> **설명:**<br/> 각 개별 컨텐츠당 예상되는 비디오 또는 오디오 스트림의 수입니다. 이 값은 재생 시간(컨텐츠 + 광고 수) 30분마다 증가합니다. 고객이 보고에 사용할 수 있는 값을 갖도록 고유한 처리 규칙을 만들어야 합니다. <br/><br/>스트림은 다음과 유사한 유사한 (또는 Totaltimeplayed `ms_s` = 비디오 총 시간) 30 분마다 계산됩니다. <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/>사용자 지정 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. estimatedstream) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. estimatedstream) </li> </ul> |

### 일시 중지된 영향을 받은 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.6 </li> <li> **샘플 값:**<br/>TRUE </li> <li> **설명:**<br/> 이 값은 true 또는 false 입니다. 단일 미디어 항목 재생 중 한 번 이상의 일시 정지가 발생한 경우에는 true입니다.  <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트 비트:**<br/> (s: 이벤트:<br/>type = pause) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>일시 정지의 영향을 받은 스트림 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. pause) </li> <li> **데이터 피드:**<br/>videopause </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pause) </li> </ul> |

### 일시 중지 이벤트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.6 </li> <li> **샘플 값:**<br/>2 </li> <li> **설명:**<br/> 이 지표는 재생 세션 중에 발생한 일시 중지 기간 수로 계산됩니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트 비트:**<br/> (s: 이벤트:<br/>type = pause) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>이벤트 일시 중단 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. pausecount) </li> <li> **데이터 피드:**<br/>videopausecount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pauseCount) </li> </ul> |

### 총 일시 중지 기간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.6 </li> <li> **샘플 값:**<br/>190 </li> <li> **설명:**<br/> 일시 중지 유형의 모든 이벤트 지속 시간 (초) 를 합계합니다. 값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다. <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>총 일시 중단 기간 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. pausetime) </li> <li> **데이터 피드:**<br/>videopausetime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pauseTime) </li> </ul> |

### 컨텐츠 다시 시작

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/> **media.resume** </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.6 </li> <li> **샘플 값:**<br/>TRUE </li> <li> **설명:**<br/> 30 분 이상 경과된 후 다시 시작하는 각 재생 횟수, 일시 중지 또는 종료 시간 또는 Videoinfo trackplay의 플레이어에서 이 값을 설정한 경우 다시 시작됩니다. <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트 비트:**<br/> (s: 이벤트:<br/>type = resume) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>컨텐츠 재개 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. resume) </li> <li> **데이터 피드:**<br/>videoresume </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.resume) </li> </ul> |

### 컨텐츠 세그먼트 보기 수

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>TRUE </li> <li> **설명:**<br/> 주 컨텐츠의 보기 수입니다. 본 프레임이 적어도 한 개 있는 경우 컨텐츠 세그먼트 보기가 카운트됩니다.  <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다. </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>컨텐츠 세그먼트 보기 수 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. segmentview) </li> <li> **데이터 피드:**<br/>videosegmentviews </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.segmentView) </li> </ul> |

## 관련 API {#section_Related_APIs}

### createMediaObject APIs {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig APIs {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)

