---
seo-title: 오디오 및 비디오 매개 변수
title: 오디오 및 비디오 매개 변수
uuid: fdacfb8b-db3e-46fb-b9ad-c3a74955b2a
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# 오디오 및 비디오 매개 변수{#audio-and-video-parameters}

>[!IMPORTANT]
>
>2019년 2월 7일, 비디오 및 오디오용 Adobe Analytics에서 지표 이름 변경을 발표했습니다. <i>Media Initiates</i>의 이름이 <i>Media Starts</i>로 변경됩니다. 이 변경 사항은 지표 및 보고에서 업계 표준을 반영하고, 보고서에서 지표를 쉽게 식별할 수 있도록 하기 위해 수행되었습니다.

>[!NOTE]
>
>2018년 9월 13일부터 비디오 및 오디오 분석에 대한 크로스 컨텐츠 추적을 허용하도록 일부 차원, 지표 및 보고서에 대한 레이블이 변경되었습니다. 이러한 레이블로는 *비디오 시작*&#x200B;이 *미디어 시작*&#x200B;으로, *비디오 길이*&#x200B;가 *컨텐츠 길이*&#x200B;로, *비디오 이름*&#x200B;이 *컨텐츠 이름*&#x200B;으로 변경되었습니다. Reports &amp; Analytics의 비디오 보고서는 모두 이름을 "비디오"가 아닌 "미디어"를 사용하도록 업데이트되었습니다. 레이블 변경으로 데이터 수집 또는 히스토리 데이터가 변경되지는 않았습니다. Report Builder나 이러한 변경의 영향을 받을 수 있는 다른 외부의 자동화된 데이터 가져오기에서 이러한 레이블을 사용하는 경우에 대비해 이러한 변경 내용을 적어 두십시오.

이 항목에서는 컨텍스트 데이터 값을 포함하여 Adobe에서 솔루션 변수를 통해 수집하는 오디오 및 비디오 컨텐츠 데이터의 목록을 제공합니다.

테이블 데이터 설명:

* **구현:**&#x200B;구현 값 및 요구 사항에 대한 정보
   * *키* - 앱에서 수동으로 설정하거나 Adobe Media SDK에 의해 자동으로 설정된 변수.
   * *필수* - 기본 오디오 및 비디오 추적에 매개 변수가 필요한지 여부를 나타냅니다.
   * *유형* - 설정할 변수의 유형(문자열 또는 숫자)을 지정합니다.
   * *전송 대상* - 데이터가 전송될 시기를 나타냅니다.Media *Start* 는 미디어 시작 시 전송되는 분석 호출이며, *광고* 시작은 광고 시작 시 전송되는 분석 호출입니다.닫기 *호출은* 하트비트 서버에서 미디어 세션 종료 시 또는 광고 종료, 장 등 분석 서버로 직접 전송되는 컴파일된 분석 호출입니다. 닫기 호출은 네트워크 패킷 호출에서 사용할 수 없습니다.
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
>보고/예약 변수에 "분류"로 설명된 아래 나열된 변수에 대한 분류 이름을 변경하지 마십시오.\
>미디어 분류는 보고서 세트가 미디어 추적을 활성화될 때 정의됩니다. Adobe는 수시로 새 속성을 추가하고, 이 경우 고객은 보고서 세트를 다시 활성화하여 새로운 미디어 속성에 액세스해야 합니다. 업데이트 프로세스 동안 Adobe는 변수의 이름을 확인하여 분류를 사용할지 여부를 결정합니다. 누락된 항목이 있으면 Adobe는 누락된 항목을 다시 추가합니다.

## 코어 오디오 및 비디오 데이터 {#core-audio-and-video-data}

### 스트림 유형 {#stream-type}

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.streamType </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소.** SDK 버전:2.2 <br/><br/>Media [Collection API](/help/media-collection-api/mc-api-overview.md) 개요 또는 SDK [다운로드 -](/help/sdk-implement/download-sdks.md)버전 2.2.  </li>  <li> **샘플 값:** <br/>"video" </li> <li> ****<br/> 설명:스트림 유형을 식별합니다. 유효한 값은 "audio", "video", ""입니다.  <br/><br/>[세그먼트 보고](/help/metrics-and-metadata/segments.md):미디어 <br/><br/>스트림 유형:모두 - <br/>모든 미디어 스트림 데이터 세그먼트;규칙:컨텐트(ID)가 <br/><br/>있는 미디어 스트림 유형:오디오 - <br/>모든 오디오 스트림 데이터 세그먼트;규칙:컨텐츠(ID)가 존재하며 미디어 스트림 유형 = 오디오 <br/><br/>미디어 스트림 유형:"비디오" - <br/>모든 비디오 스트림 데이터를 세그먼트화합니다.규칙:콘텐츠(ID)가 존재하며 미디어 스트림 유형 != audio <br/><br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.streamType) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.streamType) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>방문 시 </li> <li> **보고서 이름:**<br/>컨텐츠 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.streamType) </li> <li> **데이터 피드:** <br/>videostreamtype </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### 컨텐츠 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.id </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>"4586695ABC" </li> <li>****<br/> 설명:다른 업계/CMS ID에 다시 연결하는 데 사용할 수 있는 컨텐츠의 컨텐츠 ID는 `s:asset:video_id.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.name) </li> <li> ****<br/> 하트비트:(s:asset:video_id) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>방문 시 </li> <li> **보고서 이름:**<br/>컨텐츠 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.name) </li> <li> **데이터 피드:**<br/>비디오 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 컨텐츠 길이(변수)

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.length </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:VOD:128년;라이브:86400년;선형:1800년. </li><li> ****<br/> 설명:클립 길이/런타임 - 소비되는 컨텐츠의 최대 길이(초)입니다. It equals the last value of `l:asset:length` from events of type Main. <br/>이 `l:asset:length` 설정되지 않으면 마지막 값이 `l:asset:duration` 사용됩니다. <br/>보고에서 "비디오 길이"는 분류이고 "컨텐츠 길이(변수)"는 eVAR입니다.  <br/> **중요:** 이 속성은 진행 추적 지표 및 대상 평균 시간과 같은 여러 지표를 계산하는 데 사용됩니다. 이 값이 설정되지 않았거나 0보다 크지 않으면 이러한 지표를 사용할 수 없습니다.  알 수 없는 기간이 있는 라이브 미디어의 경우 기본값은 86400입니다. <br/>버전 1.5.1 이전 버전, `l:asset:duration`다음과 같습니다.after 1.5.1, this is `l:asset:length.`<br/> **릴리스 날짜: 2018년 9월 13일** </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.length) </li> <li> ****<br/> 하트비트:(l:asset:length) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> 컨텐츠 길이(변수) </li> <li> ****<br/> 컨텍스트 데이터:(a.media.length) </li> <li> **데이터 피드:**<br/>videolength </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 비디오 길이

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.length </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:VOD:128년;라이브:86400년;선형:1800년. </li> <li> ****<br/> 설명:클립 길이/런타임 - 소비되는 컨텐츠의 최대 길이(초)입니다. It equals the last value of `l:asset:length` from events of type Main. If `l:asset:length` is not set, then the last value of `l:asset:duration` is used. 보고에서 "비디오 길이"는 분류이고 "컨텐츠 길이(변수)"는 eVAR입니다.  <br/> **중요:** 이 속성은 진행 추적 지표 및 대상 평균 시간과 같은 여러 지표를 계산하는 데 사용됩니다. 이 값이 설정되지 않았거나 0보다 크지 않으면 이러한 지표를 사용할 수 없습니다.  알 수 없는 기간이 있는 라이브 미디어의 경우 기본값은 86400입니다. Pre Version 1.5.1, this was `l:asset:duration`; after 1.5.1, this is `l:asset:length.`<br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.length) </li> <li> ****<br/> 하트비트:(l:asset:length) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> 비디오 길이 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.length) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 컨텐츠 유형

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.contentType </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>제한된 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>"vod" </li> <li> ****<br/> 설명:스트림 유형당 사용 가능한 **값**: <br/> _오디오:_ "song", "podcast", "audiobook", "radio" <br/> __ 비디오:"VoD", "Live", "Linear", "UGC", "DVoD" <br/> 고객은 이 매개 변수에 대한 사용자 정의 값을 제공할 수 있습니다. 이것은 `s:stream:type.` 설정이 해제된 경우 `missing_content_type.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.contentType) </li> <li> ****<br/> 하트비트:(s:stream:type) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>컨텐츠 유형 </li> <li> ****<br/> 컨텍스트 데이터:(a.contentType) </li> <li> **데이터 피드:**<br/>videocontenttype </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### 미디어 세션 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>백엔드에서 가져옴 </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.8 </li> <li> **샘플 값:**<br/>1482236761294786918253 </li> <li> ****<br/> 설명:개별 재생에 고유한 컨텐츠 스트림 인스턴스를 식별합니다.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.vsid) </li> <li> ****<br/> 하트비트:(s:event:sid) </li> </ul> | <ul> <li> **사용 가능:**<br/>처리 규칙 사용 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/>사용자 지정 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.vsid) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.vsid) </li> </ul> |

### 미디어 다운로드 플래그

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> `config.downloadedcontent` </li> <li> **API 키:**<br/>백엔드에서 가져옴 </li> <li> **필수:**<br/>아니요 </li> <li> ****<br/> 유형:boolean </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소.** SDK 버전:Android <br/>및 iOS 확장 v1.1.0 실행 </li> <li> ****<br/> 샘플 값:true </li> <li> ****<br/> 설명:다운로드한 컨텐츠 미디어 세션을 재생하여 히트가 생성되면 true로 설정합니다. 다운로드된 콘텐트가 재생되지 않을 때 나타나지 않습니다.<br/><br/>[시작](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker-with-optional-configuration)  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.downloaded) </li> <li> ****<br/> 하트비트:(s:meta:a.media.downloaded) </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/>사용자 지정 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.downloaded) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.downloaded) </li> </ul> |

### 컨텐츠 플레이어 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **API 키:**<br/>media.playerName </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:"Brightcove" </li> <li> ****<br/> 설명:플레이어의 이름입니다.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.<br/>playerName) </li> <li> ****<br/> 하트비트:(s:sp:player_name) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>컨텐츠 플레이어 이름 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.playerName) </li> <li> **데이터 피드:**<br/>videoplayername </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.playerName) </li> </ul> |

### 컨텐츠 채널

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **API 키:**<br/>media.channel </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>"Sports" </li> <li> ****<br/> 설명:배포 스테이션/채널 또는 컨텐츠가 재생되는 위치. 여기에 모든 문자열 값이 허용됩니다.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.channel) </li> <li> ****<br/> 하트비트:(s:sp:channel) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>컨텐츠 채널 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.channel) </li> <li> **데이터 피드:**<br/>videochannel </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.channel) </li> </ul> |

### 컨텐츠 세그먼트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:"0-10" </li> <li> ****<br/> 설명:본 컨텐츠의 일부를 설명하는 간격(분 단위). 세그먼트는 재생 세션 중 최대 및 최소 플레이헤드 값으로 계산됩니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>컨텐츠 세그먼트 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.segment) </li> <li> **데이터 피드:**<br/>videosegment </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.segment) </li> </ul> |

### 컨텐츠 이름(변수)

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [이름](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.name </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.1 </li> <li> **샘플 값:**<br/>"The Big Bang Theory" </li> <li> **설명:**<br/>이것은 컨텐츠의 "친숙한"(사람이 읽을 수 있음) 이름으로서, `s:asset:name.`<br/>보고서의 마지막 값과 같으며, 비디오 이름은 분류이고, 컨텐트 이름(변수)은 eVAR입니다. <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.<br/>friendlyName) </li> <li> ****<br/> 하트비트:(s:asset:name) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> 컨텐츠 이름(변수) </li> <li> ****<br/> 컨텍스트 데이터:(a.media.friendlyName) </li> <li> **데이터 피드:**<br/>videoname </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 비디오 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [이름](./audio-video-parameters.md#config-media-object) </li> <li> **API 키:**<br/>media.name </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.1 </li> <li> **샘플 값:**<br/>"The Big Bang Theory" </li> <li> ****<br/> 설명:이것은 "친숙한"(사람이 읽을 수 있음) 컨텐츠 이름으로서, `s:asset:name.` 비디오 <br/>이름은 분류이고 컨텐츠 이름(변수)은 eVAR입니다.  <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.<br/>friendlyName) </li> <li> ****<br/> 하트비트:(s:asset:name) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> 비디오 이름 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.friendlyName) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

### 비디오 경로

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>"4586695ABC" </li> <li> ****<br/> 설명:사이트 및/또는 앱에서 뷰어의 경로를 추적하여 특정 비디오를 보는 데 사용한 경로를 확인할 수 있는 기능을 제공합니다. 모든 정수 및/또는 문자 조합입니다.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.name) </li> <li> ****<br/> 하트비트:(s:asset:video_id) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>prop </li> <li> **보고서 이름:**<br/>비디오 경로 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.name) </li> <li> **데이터 피드:**<br/>videopath </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.name) </li> </ul> |

### SDK 버전

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **API 키:**<br/>media.sdkVersion </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>"2.62.0_release" </li> <li> ****<br/> 설명:플레이어에서 사용하는 SDK 버전. 플레이어에 적합한 사용자 지정 값을 가질 수 있습니다. <br/><br/>고객이 보고에 사용할 수 있는 값을 갖도록 고유한 처리 규칙을 만들어야 합니다.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.<br/>sdkVersion) </li> <li> ****<br/> 하트비트:(s:sp:sdk) </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/> </li> <li> ****<br/> 컨텍스트 데이터:(a.media.sdkVersion) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### VHL 버전

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>"js-2.0.1.88-c8c0b1" </li> <li> ****<br/> 설명:추적 세션에 사용되는 미디어 SDK 버전. <br/><br/>고객이 보고에 사용할 수 있는 값을 갖도록 고유한 처리 규칙을 만들어야 합니다.  <br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.<br/>vhlVersion) </li> <li> ****<br/> 하트비트:(s:sp:hb_version) </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/>사용자 지정 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.vhlVersion) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## 표준 오디오 및 비디오 메타데이터 {#standard-audio-and-video-metadata}

### 표시

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>SHOW </li> <li> **API 키:**<br/>media.show </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> ****<br/> 샘플 값:현대 가족 블랙 리스트 뉴 걸 </li> <li> ****<br/> 설명:프로그램/시리즈 <br/>이름 프로그램 이름은 쇼가 시리즈의 일부인 경우에만 필요합니다.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.show) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.show) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>표시 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.show) </li> <li> **데이터 피드:**<br/>videoshow </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.show) </li> </ul> |

### 스트림 형식

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>STREAM_FORMAT </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>"Live" </li> <li> ****<br/> 설명:스트림 형식(라이브, VOD, 선형)입니다.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.format) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.format) </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/>사용자 지정 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.format) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.format) </li> </ul> |

### 시즌

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>SEASON </li> <li> **API 키:**<br/>media.season </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>"2" </li> <li> ****<br/> 설명:쇼가 속한 시즌 번호입니다.  시즌 시리즈는 쇼가 시리즈의 일부인 경우에만 필요합니다.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.season) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.season) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>시즌 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.season) </li> <li> **데이터 피드:**<br/>videoseason </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.season) </li> </ul> |

### 에피소드

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>EPISODE </li> <li> **API 키:**<br/>media.episode </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>"13" </li> <li> ****<br/> 설명:에피소드 번호입니다.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.episode) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.episode) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>에피소드 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.episode) </li> <li> **데이터 피드:**<br/>videoepisode </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.episode) </li> </ul> |

### 자산 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>ASSET_ID </li> <li> **API 키:**<br/>media.assetId </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>"89745363" </li> <li> ****<br/> 설명:이것은 TV 시리즈 에피소드 식별자, 동영상 자산 식별자 또는 라이브 이벤트 식별자와 같은 미디어 자산의 컨텐츠에 대한 고유 식별자입니다. 일반적으로 이러한 ID는 EIDR, TMS/Gracenote 또는 Rovi와 같은 메타데이터 권한에서 파생됩니다. 이러한 식별자는 다른 소유 시스템이나 사내 시스템에서 파생될 수도 있습니다.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.asset) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.asset) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/> 자산 ID </li> <li> ****<br/> 컨텍스트 데이터:(a.media.asset) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.asset) </li> </ul> |

### 장르

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>GENRE </li> <li> **API 키:**<br/>media.genre </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> ****<br/> 샘플 값:드라마, 코미디 </li> <li> ****<br/> 설명:컨텐츠 제작자가 정의한 컨텐츠 유형 또는 그룹화 값은 변수 구현에서 쉼표로 구분해야 합니다. 보고에서 List eVar는 각 라인 항목이 동일한 지표 가중치를 받는 라인 항목으로 각 값을 나눕니다.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.genre) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.genre) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>List eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>장르 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.genre) </li> <li> **데이터 피드:**<br/>videogenre </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.genre) </li> </ul> |

### 최초 방송 날짜

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>FIRST_AIR_DATE </li> <li> **API 키:**<br/>media.firstAirDate </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> ****<br/> 샘플 값:"2016-01-25" </li> <li> ****<br/> 설명:컨텐츠가 처음 TV로 방송된 날짜입니다. 모든 날짜 형식이 허용되지만, Adobe는 YYYY-MM-DD 형식을 권장합니다. </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.airDate) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.airDate) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> 최초 방송 날짜 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.airDate) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.airDate) </li> </ul> |

### 최초 디지털 날짜

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>FIRST_DIGITAL_DATE </li> <li> **API 키:**<br/>media.firstDigitalDate </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> ****<br/> 샘플 값:"2016-01-25" </li> <li> ****<br/> 설명:컨텐츠가 디지털 채널 또는 플랫폼에서 처음 방송된 날짜입니다. 모든 날짜 형식이 허용되지만, Adobe는 YYYY-MM-DD 형식을 권장합니다. </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.digitalDate) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.digitalDate) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/> 최초 디지털 날짜 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.digitalDate) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.digitalDate) </li> </ul> |

### 컨텐츠 등급

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>RATING </li> <li> **API 키:**<br/>media.rating </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> ****<br/> 샘플 값:TVY, TVG, TVPG, TVMA </li> <li> ****<br/> 설명:TV 보호자 지침에 정의된 등급.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.rating) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.rating) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/> 컨텐츠 등급 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.rating) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.rating) </li> </ul> |

### 작성자

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>ORIGINATOR </li> <li> **API 키:**<br/>media.originator </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> ****<br/> 샘플 값:"Warner Brothers", "Sony", "Disney" </li> <li> ****<br/> 설명:콘텐츠 제작  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.originator) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.originator) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/> 작성자 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.originator) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.originator) </li> </ul> |

### 네트워크

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>NETWORK </li> <li> **API 키:**<br/>media.network </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> ****<br/> 샘플 값:"폭스", "브라보", "ESPN" </li> <li> ****<br/> 설명:네트워크/채널 이름.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.network) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.network) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>네트워크 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.network) </li> <li> **데이터 피드:**<br/>videonetwork </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.network) </li> </ul> |

### 표시 유형

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>SHOW_TYPE </li> <li> **API 키:**<br/>media.showType </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> ****<br/> 샘플 값:"0" = 전체 에피소드;"1" = 미리 보기/트레일러;"2" = 클립;"3" = 기타. </li> <li> ****<br/> 설명:0에서 3 사이의 정수로 표현되는 컨텐츠 유형입니다.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.type) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.type) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>표시 유형 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.type) </li> <li> **데이터 피드:**<br/>videoshowtype </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>MVPD </li> <li> **API 키:**<br/>media.pass.mvpd </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> ****<br/> 샘플 값:"Comcast", "DirecTV", "Dish" </li> <li> ****<br/> 설명:Adobe 인증을 통해 제공된 MVPD.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.pass.mvpd) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.pass.<br/>mvpd) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>MVPD </li> <li> ****<br/> 컨텍스트 데이터:(a.media.pass.mvpd) </li> <li> **데이터 피드:**<br/>videomvpd </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### 인증됨

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>AUTHORIZED </li> <li> **API 키:**<br/>media.pass.auth </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> ****<br/> 샘플 값:"TRUE" </li> <li> ****<br/> 설명:사용자가 Adobe 인증을 통해 인증되었습니다.  <br/>**중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.pass.auth) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.pass.<br/>auth) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>인증됨 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.pass.auth) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pass.auth) </li> </ul> |

### 방송 시간대

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>DAY_PART </li> <li> **API 키:**<br/>media.dayPart </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> </li> <li> ****<br/> 설명:컨텐츠가 브로드캐스트되거나 재생되는 시간을 정의하는 속성입니다. 이는 고객이 필요에 따라 모든 값을 설정할 수 있습니다.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.dayPart) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.dayPart) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>방송 시간대 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.dayPart) </li> <li> **데이터 피드:**<br/>videodaypart </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.dayPart) </li> </ul> |

### 미디어 피드 유형

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>FEED </li> <li> **API 키:**<br/>media.feed </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> ****<br/> 샘플 값:"East-HD", "West-HD", "East-SD" </li> <li> ****<br/> 설명:피드 유형입니다.  <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.feed) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.feed) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> 미디어 피드 유형 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.feed) </li> <li> **데이터 피드:**<br/>videofeedtype </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.feed) </li> </ul> |

### 아티스트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.artist </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소.** SDK 버전:1.5.7 <br/>Media [Collection 개요](/help/media-collection-api/mc-api-overview.md) 또는 SDK [다운로드 - 버전 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **샘플 값:** <br/>"The Beatles" </li> <li> ****<br/> 설명:아티스트의 이름입니다.  <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.artist) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.artist) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> </li> <li> ****<br/> 컨텍스트 데이터:(a.media.artist) </li> <li> **데이터 피드:** <br/>videoaudioartist </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.artist) </li> </ul> |

### 앨범

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.album </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소.** SDK 버전:1.5.7 <br/>Media [Collection 개요](/help/media-collection-api/mc-api-overview.md) 또는 SDK [다운로드 - 버전 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **샘플 값:**<br/>"Revolver" </li> <li> ****<br/> 설명:앨범의 이름입니다.  <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.album) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.album) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> </li> <li> ****<br/> 컨텍스트 데이터:(a.media.album) </li> <li> **데이터 피드:** <br/>videoaudioalbum </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.album) </li> </ul> |

### 레이블

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.label </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소.** SDK 버전:1.5.7 <br/>Media [Collection 개요](/help/media-collection-api/mc-api-overview.md) 또는 SDK [다운로드 - 버전 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **샘플 값:**<br/>"Revolver" </li> <li> ****<br/> 설명:레코드 레이블의 이름입니다.  <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.label) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.label) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> </li> <li> ****<br/> 컨텍스트 데이터:(a.media.label) </li> <li> **데이터 피드:** <br/>videoaudiolabel </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.label) </li> </ul> |

### Author

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.author </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소.** SDK 버전:1.5.7 <br/>Media [Collection 개요](/help/media-collection-api/mc-api-overview.md) 또는 SDK [다운로드 - 버전 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **샘플 값:** <br/>"John Kennedy Toole" </li> <li> ****<br/> 설명:작성자 이름(오디오 책).  <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.author) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.author) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> </li> <li> ****<br/> 컨텍스트 데이터:(a.media.author) </li> <li> **데이터 피드:** <br/>videoaudioauthor </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.author) </li> </ul> |

### 방송국

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.station </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소.** SDK 버전:1.5.7 <br/>Media [Collection 개요](/help/media-collection-api/mc-api-overview.md) 또는 SDK [다운로드 - 버전 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **샘플 값:** <br/>"NPR" </li> <li> ****<br/> 설명:라디오 방송국의 이름/ID.  <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.station) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.station) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> </li> <li> ****<br/> 컨텍스트 데이터:(a.media.station) </li> <li> **데이터 피드:**<br/>videoaudiostation </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.station) </li> </ul> |

### 게시자

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.publisher </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 시작, 미디어 닫기 </li> <li> **최소.** SDK 버전:1.5.7 <br/>Media [Collection 개요](/help/media-collection-api/mc-api-overview.md) 또는 SDK [다운로드 - 버전 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **샘플 값:** <br/>"Random Bauhaus" </li> <li> ****<br/> 설명:오디오 콘텐트 게시자의 이름입니다.  <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.publisher) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.publisher) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> </li> <li> ****<br/> 컨텍스트 데이터:(a.media.publisher) </li> <li> **데이터 피드:**<br/>videoaudiopublisher </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.publisher) </li> </ul> |

## 오디오 및 비디오 지표 {#audio-and-video-metrics}

### 미디어 시작

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/> 문자열</li> <li> ****<br/> 전송 대상:미디어 시작</li> <li> **최소. SDK 버전:**&#x200B;모두</li> <li> **샘플 값:**<br/>TRUE </li> <li> ****<br/> 설명:미디어에 대한 이벤트를 로드합니다. 이 이벤트는 뷰어가 _재생_ 단추를 클릭할 때 발생합니다. 이 이벤트는 프리롤 광고, 버퍼링, 오류 등이 있는 경우에도 계산됩니다.  <br/>**중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.view) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=start) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> ****<br/> 보고서 이름:미디어 시작 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.view) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.view) </li> </ul> |

### 컨텐츠 시작

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>TRUE </li> <li> ****<br/> 설명:미디어의 첫 번째 프레임이 사용됩니다. 광고, 버퍼링 중에 사용자가 그만두면 "컨텐츠 시작" 이벤트가 일어나지 않습니다.  <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>컨텐츠 시작 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.play) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.play) </li> </ul> |

### 컨텐츠 완료 {#content-complete}

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>TRUE </li> <li> ****<br/> 설명:완성을 위해 관찰된 스트림. 이는 사용자가 전체 스트림을 보거나 청취할 필요가 없다는 것을 의미하지는 않습니다.그들은 앞으로를 건너뛸 수도 있었다. 이는 사용자가 스트림의 끝에 100%만 도달했음을 의미합니다. <br/>세션 [종료도 참조하십시오](quality-parameters.md#session-end)<br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> ****<br/> 하트비트:(s:event:<br/>type=complete) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>컨텐츠 완료 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.complete) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.complete) </li> </ul> |

### 컨텐츠 체류 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>105 </li> <li> ****<br/> 설명:기본 컨텐츠에서 PLAY 유형의 모든 이벤트에 대한 이벤트 지속 시간(초)을 합산합니다.  값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다.  <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>컨텐츠 체류 시간 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.timePlayed) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.timePlayed) </li> </ul> |

### 미디어 사용 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>120 </li> <li> ****<br/> 설명:PLAY 유형의 모든 이벤트(기본 및 광고 컨텐츠 모두)에 대한 이벤트 지속 시간(초)을 합산합니다.  값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다.  <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/> 미디어 사용 시간 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.totalTimePlayed) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### 재생된 고유 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>94 </li> <li> ****<br/> 설명:세션 중에 재생된 컨텐츠의 고유한 세그먼트 값(초)입니다. 시청자가 컨텐츠에서 동일한 세그먼트를 여러 번 본다는 다시 찾기 시나리오에서 재생되는 시간은 제외합니다.  값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다.  <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>사용자 지정 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.uniqueTimePlayed) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.uniqueTimePlayed) </li> </ul> |

### 10% 진행률 마커

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>TRUE </li> <li> ****<br/> 설명:재생 헤드는 길이를 기반으로 컨텐츠의 10% 마커를 전달합니다. 마커는 역방향을 찾으려는 경우에도 한 번만 계산됩니다. 정방향으로 찾는 경우 건너뛴 마커는 계산되지 않습니다.  <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>10% 진행률 마커 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.progress10) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.progress10) </li> </ul> |

### 25% 진행률 마커

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>TRUE </li> <li> ****<br/> 설명:재생 헤드는 콘텐트 길이를 기준으로 25% 마커를 전달합니다. 마커는 역방향을 찾으려는 경우에도 한 번만 계산됩니다. 정방향으로 찾는 경우 건너뛴 마커는 계산되지 않습니다.  <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>25% 진행률 마커 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.progress25) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.progress25) </li> </ul> |

### 50% 진행률 마커

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>TRUE </li> <li> ****<br/> 설명:재생 헤드는 콘텐트 길이를 기준으로 50% 마커를 전달합니다. 마커는 역방향을 찾으려는 경우에도 한 번만 계산됩니다. 정방향으로 찾는 경우 건너뛴 마커는 계산되지 않습니다.  <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>50% 진행률 마커 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.progress50) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.progress50) </li> </ul> |

### 75% 진행률 마커

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/> **N/A** </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>TRUE </li> <li> ****<br/> 설명:재생 헤드는 컨텐츠 길이에 따라 75% 마커를 전달합니다. 마커는 역방향을 찾으려는 경우에도 한 번만 계산됩니다. 정방향으로 찾는 경우 건너뛴 마커는 계산되지 않습니다.  <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>75% 진행률 마커 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.progress75) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.progress75) </li> </ul> |

### 95% 진행률 마커

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>TRUE </li> <li> ****<br/> 설명:재생 헤드는 컨텐츠 길이에 따라 95% 컨텐츠 마커를 전달합니다. 마커는 역방향을 찾으려는 경우에도 한 번만 계산됩니다. 정방향으로 찾는 경우 건너뛴 마커는 계산되지 않습니다.  <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>95% 진행률 마커 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.progress95) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.progress95) </li> </ul> |

### Average Minute Audience

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>1보다 크거나 같음 </li> <li> ****<br/> 설명:평균 대상(분) 지표는 하나의 특정 미디어 항목에 대한 총 컨텐츠 체류 시간으로 계산되며 모든 재생 세션에 대한 길이로 구분됩니다. <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>대상 평균 시간(분) </li> <li> ****<br/> 컨텍스트 데이터:(a.media.averageMinuteAudience) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### 통합 데이터

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> ****<br/> 유형:boolean </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:true  </li> <li> ****<br/> 설명:히트가 페더레이션되면 true로 설정합니다(즉, 고객이 자체 구현이 아니라 통합 데이터 공유의 일부로 수신함). </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/>N/A </li> <li> ****<br/> 컨텍스트 데이터:(a.media.federated) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.federated) </li> </ul> |

### 예상 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:1 - 19분 재생 <br/>2 - 31분 재생 <br/>3 - 78분 재생 </li> <li> ****<br/> 설명:각 개별 컨텐츠당 예상 비디오 또는 오디오 스트림 수입니다. 이 값은 재생 시간(컨텐츠 + 광고 수) 30분마다 증가합니다. 고객이 보고에 사용할 수 있는 값을 갖도록 고유한 처리 규칙을 만들어야 합니다. <br/><br/>스트림은 다음과 유사한 `ms_s` (또는 totalTimePlayed = 비디오 총 시간)을 기준으로 30분마다 계산됩니다. <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/>사용자 지정 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.estimatedStreams) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.estimateStreams) </li> </ul> |

### 일시 중지된 영향을 받은 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.6 </li> <li> **샘플 값:**<br/>TRUE </li> <li> ****<br/> 설명:이 값은 true 또는 false입니다. 단일 미디어 항목 재생 중 한 번 이상의 일시 정지가 발생한 경우에는 true입니다.  <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> ****<br/> 하트비트:(s:event:<br/>type=pause) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>일시 정지의 영향을 받은 스트림 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.pause) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pause) </li> </ul> |

### 일시 중지 이벤트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.6 </li> <li> **샘플 값:**<br/>2 </li> <li> ****<br/> 설명:이 지표는 재생 세션 중에 발생한 일시 중지 기간 수로 계산됩니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> ****<br/> 하트비트:(s:event:<br/>type=pause) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>이벤트 일시 중단 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.pauseCount) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pauseCount) </li> </ul> |

### 총 일시 중지 기간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.6 </li> <li> **샘플 값:**<br/>190 </li> <li> ****<br/> 설명:PAUSE 유형의 모든 이벤트의 지속 시간(초)을 합산합니다. 값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다. <br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>총 일시 중단 기간 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.pauseTime) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pauseTime) </li> </ul> |

### 컨텐츠 다시 시작

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/> **media.resume** </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:** 1.5.6 </li> <li> **샘플 값:**<br/>TRUE </li> <li> ****<br/> 설명:Resume은 30분 이상의 버퍼, 일시 중지 또는 정지 기간 OR 플레이어에서 이 값을 설정한 경우 다시 시작하는 각 재생에 대해 카운트됩니다. <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> ****<br/> 하트비트:(s:event:<br/>type=resume) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>컨텐츠 재개 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.resume) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.resume) </li> </ul> |

### 컨텐츠 세그먼트 보기 수

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>TRUE </li> <li> ****<br/> 설명:기본 컨텐츠의 보기 수입니다. 본 프레임이 적어도 한 개 있는 경우 컨텐츠 세그먼트 보기가 카운트됩니다.  <br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다. </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>컨텐츠 세그먼트 보기 수 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.segmentView) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.segmentView) </li> </ul> |

### 광고 수

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> ****<br/> SDK 키:해당 없음 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>2 </li> <li> ****<br/> 설명:미디어 세션 중에 시작된 광고 수입니다.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/>사용자 지정 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.adCount) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.adCount) </li> </ul> |

### 장 수

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> ****<br/> SDK 키:해당 없음 </li> <li> **API 키:**<br/>N/A </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:미디어 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/>2 </li> <li> ****<br/> 설명:미디어 세션 중에 시작된 장 수입니다.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **하트비트:**<br/>N/A </li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/>사용자 지정 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.chapterCount) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapterCount) </li> </ul> |

## CPA(California Consumer Privacy Act) 매개 변수 {#ccpa-params}

### 옵트아웃 서버 측 전달

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> ****<br/> SDK 키:해당 없음 </li> <li> ****<br/> API 키:analytics.optOutServerSideForwarding </li> <li> **필수:**<br/>아니요 </li> <li> ****<br/> 유형:boolean </li> <li> ****<br/> 전송 대상:미디어 시작 </li> <li> **최소.** SDK 버전:해당 없음 </li> <li> ****<br/> 샘플 값:true </li> <li>****<br/> 설명:최종 사용자가 Adobe Analytics와 다른 Experience Cloud 솔루션(예: Audience Manager) 간에 데이터를 공유하지 않기로 선택한 경우 true로 설정합니다. </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(opt.dmp) </li> <li> ****<br/> 하트비트:(s:meta:cm.ssf) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>방문 시 </li> <li> **보고서 이름:**<br/>컨텐츠 </li> <li> ****<br/> 컨텍스트 데이터:해당 없음 </li> <li> **데이터 피드:**<br/>비디오 </li> <li> ****<br/> Audience Manager:해당 없음 </li> </ul> |

### 옵트아웃 공유

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> ****<br/> SDK 키:해당 없음 </li> <li> ****<br/> API 키:analytics.optOutShare </li> <li> **필수:**<br/>아니요 </li> <li> ****<br/> 유형:boolean </li> <li> ****<br/> 전송 대상:미디어 시작 </li> <li> **최소.** SDK 버전:해당 없음 </li> <li> ****<br/> 샘플 값:true </li> <li>****<br/> 설명:최종 사용자가 자신의 데이터를 페더레이션되지 않도록 선택한 경우(예: 다른 Adobe Analytics 클라이언트로 이동) true로 설정합니다. </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(opt.oos) </li> <li> ****<br/> 하트비트:(s:meta:cm.oos) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>방문 시 </li> <li> **보고서 이름:**<br/>컨텐츠 </li> <li> ****<br/> 컨텍스트 데이터:해당 없음 </li> <li> **데이터 피드:**<br/>비디오 </li> <li> ****<br/> Audience Manager:해당 없음 </li> </ul> |

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

