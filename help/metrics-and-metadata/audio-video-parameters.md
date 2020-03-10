---
title: 오디오 및 비디오 매개 변수
description: null
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
translation-type: tm+mt
source-git-commit: cebf5697e3746721d29bfaa5356d5a2748fea435

---


# 오디오 및 비디오 매개 변수{#audio-and-video-parameters}

>[!IMPORTANT]
>
>2019년 2월 7일 Adobe Analytics for Video and Audio의 지표 이름이 변경되었습니다. <i>Media Initiates</i>의 이름이 <i>Media Starts</i>로 변경됩니다. 이러한 변경은 지표 및 보고와 관련한 업계 표준을 반영하며 보고에서 지표를 편리하게 식별하기 위해 수행되었습니다.

>[!NOTE]
>
>2018년 9월 13일부터 비디오 및 오디오 분석을 컨텐츠 간에 추적할 수 있도록 일부 차원, 지표 및 보고서에 대한 레이블을 변경했습니다. 이러한 레이블로는 *비디오 시작*&#x200B;이 *미디어 시작*&#x200B;으로, *비디오 길이*&#x200B;가 *컨텐츠 길이*&#x200B;로, *비디오 이름*&#x200B;이 *컨텐츠 이름*&#x200B;으로 변경되었습니다. Reports &amp; Analytics의 비디오 보고서는 모두 이름을 &quot;비디오&quot;가 아닌 &quot;미디어&quot;를 사용하도록 업데이트되었습니다. 레이블 변경으로 데이터 수집 또는 히스토리 데이터가 변경되지는 않았습니다. Report Builder나 이러한 변경의 영향을 받을 수 있는 다른 외부의 자동화된 데이터 가져오기에서 이러한 레이블을 사용하는 경우에 대비해 이러한 변경 내용을 적어 두십시오.

이 항목에서는 컨텍스트 데이터 값을 포함하여 Adobe에서 솔루션 변수를 통해 수집하는 오디오 및 비디오 컨텐츠 데이터의 목록을 제공합니다.

테이블 데이터 설명:

* **구현:**&#x200B;구현 값 및 요구 사항에 대한 정보
   * *키* - 앱에서 수동으로 설정하거나 Adobe Media SDK에 의해 자동으로 설정된 변수.
   * *필수* - 기본 오디오 및 비디오 추적에 매개 변수가 필요한지 여부를 나타냅니다.
   * *유형* - 설정할 변수의 유형(문자열 또는 숫자)을 지정합니다.
   * *전송 시점* - 데이터가 전송되는 시점을 나타냅니다. *미디어 시작*&#x200B;은 미디어 시작 시 분석 호출이 전송되고, *광고 시작*&#x200B;은 광고 시작 시 분석 호출이 전송됩니다. *닫기* 호출은 미디어 세션 종료 시 또는 광고, 챕터 종료 시 하트비트 서버에서 Analytics 서버로 컴파일된 분석 호출이 직접 전송됩니다. 닫기 호출은 네트워크 패킷 호출에 사용할 수 없습니다.
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
>보고/예약 변수 아래에 &quot;분류&quot;로 설명되어 있는 변수의 분류 이름을 변경하지 마십시오.\
>미디어 분류는 보고서 세트가 미디어 추적에 사용될 때 정의됩니다. Adobe는 수시로 새 속성을 추가하며, 이 경우 고객이 보고서 세트를 다시 활성화하여 새로운 미디어 속성에 액세스해야 합니다. 업데이트 프로세스 중에 Adobe는 변수의 이름을 확인하여 분류를 사용할지 여부를 결정합니다. 누락된 항목이 있을 경우 Adobe가 다시 추가합니다.

## 코어 오디오 및 비디오 데이터 {#core-audio-and-video-data}

### 스트림 유형 {#stream-type}

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.streamType</li> <li> **필수:**<br/>예</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 2.2 <br/><br/>[Media Collection API 개요](/help/media-collection-api/mc-api-overview.md) 또는 [SDK 다운로드 -버전 2.2](/help/sdk-implement/download-sdks.md)에서 사용할 수 있습니다.  </li>  <li> **샘플 값:**<br/>&quot;video&quot;</li> <li> **설명:**<br/>스트림 유형을 식별합니다. 유효한 값은 &quot;audio&quot;, &quot;video&quot;, &quot;&quot;입니다.<br/><br/>[세그먼트 보고](/help/metrics-and-metadata/segments.md):<br/><br/>미디어 스트림 유형: 모두 -<br/>모든 미디어 스트림 데이터 세그먼트화, 규칙: 컨텐츠(ID)가 있음<br/><br/>미디어 스트림 유형: 오디오 -<br/>모든 오디오 스트림 데이터 세그먼트화, 규칙: 컨텐츠(ID)가 있고 미디어 스트림 유형 = 오디오<br/><br/>미디어 스트림 유형: &quot;비디오&quot; -<br/>모든 비디오 스트림 데이터 세그먼트화, 규칙: 컨텐츠(ID)가 있고 미디어 스트림 유형!= audio<br/><br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.streamType)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.streamType)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>방문 시</li> <li> **보고서 이름:**<br/>컨텐츠</li> <li> **컨텍스트 데이터:**<br/>(a.media.streamType)</li> <li> **데이터 피드:**<br/>videostreamtype</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.streamType)</li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### 컨텐츠 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.id</li> <li> **필수:**<br/>예</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>&quot;4586695ABC&quot;</li> <li>**설명:**<br/>`s:asset:video_id.`의 마지막 값과 같은 산업/CMS ID에 다시 연결하는 데 사용할 수 있는 컨텐츠의 컨텐츠 ID입니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.name)</li> <li> **하트비트:**<br/>(s:asset:video_id)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>방문 시</li> <li> **보고서 이름:**<br/>컨텐츠</li> <li> **컨텍스트 데이터:**<br/>(a.media.name)</li> <li> **데이터 피드:**<br/>비디오</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.name)</li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 컨텐츠 길이(변수)

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.length</li> <li> **필수:**<br/>예</li> <li> **유형:**<br/>숫자</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>VOD: 128, Live: 86400; Linear: 1800.</li><li> **설명:**<br/>클립 길이/런타임 - 사용되는 컨텐츠의 최대 길이(또는 기간)입니다(초). 기본 유형의 이벤트에서`l:asset:length`의 마지막 값과 동일합니다.<br/>`l:asset:length`가 설정되지 않은 경우`l:asset:duration`의 마지막 값이 사용됩니다.<br/>보고에서 &quot;비디오 길이&quot;는 분류이고 &quot;컨텐츠 길이(변수)&quot;는 eVAR입니다.<br/> **중요:** 이 속성은 진행 추적 지표 및 대상 평균 시간과 같은 여러 지표를 계산하는 데 사용됩니다. 이 값이 설정되지 않았거나 0보다 크지 않으면 이러한 지표를 사용할 수 없습니다.  알 수 없는 기간이 있는 라이브 미디어의 경우 기본값은 86400입니다. <br/>1.5.1 이전 버전인 경우 `l:asset:duration`이고, 1.5.1 이후 버전인 경우 `l:asset:length.`입니다. <br/> **릴리스 날짜: 2018년 9월 13일** </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.length)</li> <li> **하트비트:**<br/>(l:asset:length)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>컨텐츠 길이(변수)</li> <li> **컨텍스트 데이터:**<br/>(a.media.length)</li> <li> **데이터 피드:**<br/>videolength</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.length)</li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 비디오 길이

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.length</li> <li> **필수:**<br/>예</li> <li> **유형:**<br/>숫자</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>VOD: 128, Live: 86400; Linear: 1800.</li> <li> **설명:**<br/>클립 길이/런타임 - 사용되는 컨텐츠의 최대 길이(또는 기간)입니다(초). 기본 유형의 이벤트에서`l:asset:length`의 마지막 값과 동일합니다.`l:asset:length`가 설정되지 않은 경우`l:asset:duration`의 마지막 값이 사용됩니다. 보고에서 &quot;비디오 길이&quot;는 분류이고 &quot;컨텐츠 길이(변수)&quot;는 eVAR입니다.<br/> **중요:** 이 속성은 진행 추적 지표 및 대상 평균 시간과 같은 여러 지표를 계산하는 데 사용됩니다. 이 값이 설정되지 않았거나 0보다 크지 않으면 이러한 지표를 사용할 수 없습니다.  알 수 없는 기간이 있는 라이브 미디어의 경우 기본값은 86400입니다. 1.5.1 이전 버전인 경우 `l:asset:duration`이고, 1.5.1 이후 버전인 경우 `l:asset:length.`<br/>입니다. **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.length)</li> <li> **하트비트:**<br/>(l:asset:length)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>분류</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>비디오 길이</li> <li> **컨텍스트 데이터:**<br/>(a.media.length)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.length)</li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 컨텐츠 유형

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.contentType</li> <li> **필수:**<br/>예</li> <li> **유형:**<br/>제한된 문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>&quot;vod&quot;</li> <li> **설명:**<br/>**스트림 유형&#x200B;**별 사용 가능한 값:<br/> _오디오:_ &quot;song&quot;, &quot;podcast&quot;, &quot;audiobook&quot;, &quot;radio&quot; <br/> _비디오:_ &quot;VoD&quot;, &quot;Live&quot;, &quot;Linear&quot;, &quot;UGC&quot;, &quot;DVoD&quot; <br/> 고객은 이 매개 변수에 대한 사용자 지정 값을 제공할 수 있습니다. 이것은 `s:stream:type.`입니다. 설정이 해제된 경우 `missing_content_type.`입니다. </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.contentType)</li> <li> **하트비트:**<br/>(s:stream:type)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>컨텐츠 유형</li> <li> **컨텍스트 데이터:**<br/>(a.contentType)</li> <li> **데이터 피드:**<br/>videocontenttype</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.contentType)</li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### 미디어 세션 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>백엔드에서 가져옴</li> <li> **필수:**<br/>예</li> <li> **유형:**<br/>숫자</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.8 </li> <li> **샘플 값:**<br/>1482236761294786918253</li> <li> **설명:**<br/>개별 재생에 고유한 컨텐츠 스트림의 인스턴스를 식별합니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.vsid)</li> <li> **하트비트:**<br/>(s:event:sid)</li> </ul> | <ul> <li> **사용 가능:**<br/>처리 규칙 사용</li> <li> **예약된 변수:**<br/>N/A</li> <li> **보고서 이름:**<br/>사용자 지정</li> <li> **컨텍스트 데이터:**<br/>(a.media.vsid)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.vsid)</li> </ul> |

### 미디어에서 다운로드한 플래그

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> `config.downloadedcontent` </li> <li> **API 키:**<br/>백엔드에서 가져옴</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>부울</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** <br/>Android 및 iOS 확장 프로그램 v1.1.0 실행 </li> <li> **샘플 값:**<br/>true</li> <li> **설명:**<br/>다운로드한 컨텐츠 미디어 세션 재생으로 인해 히트가 생성되면 참으로 설정합니다. 다운로드한 컨텐츠가 재생되지 않을 경우 나타나지 않습니다.<br/><br/>[Launch](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker-with-optional-configuration)</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.downloaded)</li> <li> **하트비트:**<br/>(s:meta:a.media.downloaded)</li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙</li> <li> **예약된 변수:**<br/>N/A</li> <li> **보고서 이름:**<br/>사용자 지정</li> <li> **컨텍스트 데이터:**<br/>(a.media.downloaded)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.downloaded)</li> </ul> |

### 컨텐츠 플레이어 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **API 키:**<br/>media.playerName</li> <li> **필수:**<br/>예</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>&quot;Brightcove&quot;</li> <li> **설명:**<br/>플레이어의 이름입니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.<br/>playerName)</li> <li> **하트비트:**<br/>(s:sp:player_name)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>컨텐츠 플레이어 이름</li> <li> **컨텍스트 데이터:**<br/>(a.media.playerName)</li> <li> **데이터 피드:**<br/>videoplayername</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.playerName)</li> </ul> |

### 컨텐츠 채널

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **API 키:**<br/>media.channel</li> <li> **필수:**<br/>예</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>&quot;Sports&quot;</li> <li> **설명:**<br/>배포 스테이션/채널 또는 컨텐츠가 재생되는 위치입니다. 여기에 모든 문자열 값이 허용됩니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.channel)</li> <li> **하트비트:**<br/>(s:sp:channel)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>컨텐츠 채널</li> <li> **컨텍스트 데이터:**<br/>(a.media.channel)</li> <li> **데이터 피드:**<br/>videochannel</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.channel)</li> </ul> |

### 컨텐츠 세그먼트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **필수:**<br/>예</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>&quot;0-10&quot;</li> <li> **설명:**<br/>본 컨텐츠 부분을 설명하는 간격입니다(분). 세그먼트는 재생 세션 중 최대 및 최소 플레이헤드 값으로 계산됩니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>N/A</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>컨텐츠 세그먼트</li> <li> **컨텍스트 데이터:**<br/>(a.media.segment)</li> <li> **데이터 피드:**<br/>videosegment</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.segment)</li> </ul> |

### 컨텐츠 이름(변수)

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **API 키:**<br/>media.name</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.1 </li> <li> **샘플 값:**<br/>&quot;The Big Bang Theory&quot;</li> <li> **설명:**<br/>이것은 컨텐츠의 &quot;친숙한&quot;(사람이 읽을 수 있음) 이름으로,`s:asset:name.`<br/>의 마지막 값과 같습니다. 보고 시 비디오 이름은 분류이고, 컨텐츠 이름(변수)은 eVAR입니다.<br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.<br/>friendlyName)</li> <li> **하트비트:**<br/>(s:asset:name)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>컨텐츠 이름(변수)</li> <li> **컨텍스트 데이터:**<br/>(a.media.friendlyName)</li> <li> **데이터 피드:**<br/>videoname</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.friendlyName)</li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 비디오 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **API 키:**<br/>media.name</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.1 </li> <li> **샘플 값:**<br/>&quot;The Big Bang Theory&quot;</li> <li> **설명:**<br/>이것은 컨텐츠의 &quot;친숙한&quot;(사람이 읽을 수 있음) 이름으로,`s:asset:name.`의 마지막 값과 같습니다.<br/>보고 시 비디오 이름은 분류이고, 컨텐츠 이름(변수)은 eVAR입니다.<br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.<br/>friendlyName)</li> <li> **하트비트:**<br/>(s:asset:name)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>분류</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>비디오 이름</li> <li> **컨텍스트 데이터:**<br/>(a.media.friendlyName)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.friendlyName)</li> </ul> |

### 비디오 경로

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>&quot;4586695ABC&quot;</li> <li> **설명:**<br/>사이트 및/또는 앱에서 뷰어의 경로를 추적하여 특정 비디오를 보는 데 사용한 경로를 확인할 수 있는 기능을 제공합니다. 모든 정수 및/또는 문자 조합입니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.name)</li> <li> **하트비트:**<br/>(s:asset:video_id)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>prop</li> <li> **보고서 이름:**<br/>비디오 경로</li> <li> **컨텍스트 데이터:**<br/>(a.media.name)</li> <li> **데이터 피드:**<br/>videopath</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.name)</li> </ul> |

### SDK 버전

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **API 키:**<br/>media.sdkVersion</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&quot;2.62.0_release&quot;</li> <li> **설명:**<br/>플레이어에서 사용하는 SDK 버전입니다. 플레이어에 적합한 사용자 지정 값을 가질 수 있습니다.<br/><br/>고객이 보고에 사용할 수 있는 값을 갖도록 고유한 처리 규칙을 만들어야 합니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.<br/>sdkVersion)</li> <li> **하트비트:**<br/>(s:sp:sdk)</li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙</li> <li> **예약된 변수:**<br/>N/A</li> <li> **보고서 이름:**<br/> </li> <li> **컨텍스트 데이터:**<br/>(a.media.sdkVersion)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.sdkVersion)</li> </ul> |

### VHL 버전

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&quot;js-2.0.1.88-c8c0b1&quot;</li> <li> **설명:**<br/>추적 세션에 사용되는 Media SDK 버전입니다.<br/><br/>고객이 보고에 사용할 수 있는 값을 갖도록 고유한 처리 규칙을 만들어야 합니다.<br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.<br/>vhlVersion)</li> <li> **하트비트:**<br/>(s:sp:hb_version)</li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙</li> <li> **예약된 변수:**<br/>N/A</li> <li> **보고서 이름:**<br/>사용자 지정</li> <li> **컨텍스트 데이터:**<br/>(a.media.vhlVersion)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.vhlVersion)</li> </ul> |

## 표준 오디오 및 비디오 메타데이터 {#standard-audio-and-video-metadata}

### 표시

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>SHOW</li> <li> **API 키:**<br/>media.show</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&quot;Modern Family&quot; &quot;Blacklist&quot; &quot;New Girl&quot;</li> <li> **설명:**<br/>프로그램/시리즈 이름<br/>프로그램 이름은 표시가 시리즈의 일부인 경우에만 필요합니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.show)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.show)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>표시</li> <li> **컨텍스트 데이터:**<br/>(a.media.show)</li> <li> **데이터 피드:**<br/>videoshow</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.show)</li> </ul> |

### 스트림 형식

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>STREAM_FORMAT</li> <li> **API 키:**<br/>N/A</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&quot;Live&quot;</li> <li> **설명:**<br/>스트림의 형식입니다(실시간, VOD, 선형).</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.format)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.format)</li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙</li> <li> **예약된 변수:**<br/>N/A</li> <li> **보고서 이름:**<br/>사용자 지정</li> <li> **컨텍스트 데이터:**<br/>(a.media.format)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.format)</li> </ul> |

### 시즌

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>SEASON</li> <li> **API 키:**<br/>media.season</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&quot;2&quot;</li> <li> **설명:**<br/>표시가 속한 시즌 번호입니다.  시즌 시리즈는 표시가 시리즈의 일부인 경우에만 필요합니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.season)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.season)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>시즌</li> <li> **컨텍스트 데이터:**<br/>(a.media.season)</li> <li> **데이터 피드:**<br/>videoseason</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.season)</li> </ul> |

### 에피소드

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>EPISODE</li> <li> **API 키:**<br/>media.episode</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&quot;13&quot;</li> <li> **설명:**<br/>에피소드의 번호입니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.episode)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.episode)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>에피소드</li> <li> **컨텍스트 데이터:**<br/>(a.media.episode)</li> <li> **데이터 피드:**<br/>videoepisode</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.episode)</li> </ul> |

### 자산 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>ASSET_ID</li> <li> **API 키:**<br/>media.assetId</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&quot;89745363&quot;</li> <li> **설명:**<br/>TV 시리즈 에피소드 식별자, 동영상 자산 식별자 또는 라이브 이벤트 식별자와 같은 미디어 자산 컨텐츠에 대한 고유 식별자입니다. 일반적으로 이러한 ID는 EIDR, TMS/Gracenote 또는 Rovi와 같은 메타데이터 권한에서 파생됩니다. 이러한 식별자는 다른 소유 시스템이나 사내 시스템에서 파생될 수도 있습니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.asset)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.asset)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>분류</li> <li> **보고서 이름:**<br/>자산 ID</li> <li> **컨텍스트 데이터:**<br/>(a.media.asset)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.asset)</li> </ul> |

### 장르

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>GENRE</li> <li> **API 키:**<br/>media.genre</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&quot;드라마&quot;, &quot;코메디&quot;</li> <li> **설명:**<br/>컨텐츠 생성자가 정의한 컨텐츠 유형 또는 그룹입니다. 값은 변수 구현에서 쉼표로 구분해야 합니다. 보고에서 List eVar는 각 라인 항목이 동일한 지표 가중치를 받는 라인 항목으로 각 값을 나눕니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.genre)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.genre)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>List eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>장르</li> <li> **컨텍스트 데이터:**<br/>(a.media.genre)</li> <li> **데이터 피드:**<br/>videogenre</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.genre)</li> </ul> |

### 최초 방송 날짜

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>FIRST_AIR_DATE</li> <li> **API 키:**<br/>media.firstAirDate</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&quot;2016-01-25&quot;</li> <li> **설명:**<br/>컨텐츠가 TV에 처음 방송된 날짜입니다. 모든 날짜 형식이 허용되지만, Adobe는 YYYY-MM-DD 형식을 권장합니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.airDate)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.airDate)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>분류</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>최초 방송 날짜</li> <li> **컨텍스트 데이터:**<br/>(a.media.airDate)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.airDate)</li> </ul> |

### 최초 디지털 날짜

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>FIRST_DIGITAL_DATE</li> <li> **API 키:**<br/>media.firstDigitalDate</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&quot;2016-01-25&quot;</li> <li> **설명:**<br/>컨텐츠가 디지털 채널 또는 플랫폼에서 처음으로 방송된 날짜입니다. 모든 날짜 형식이 허용되지만, Adobe는 YYYY-MM-DD 형식을 권장합니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.digitalDate)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.digitalDate)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>분류</li> <li> **보고서 이름:**<br/>최초 디지털 날짜</li> <li> **컨텍스트 데이터:**<br/>(a.media.digitalDate)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.digitalDate)</li> </ul> |

### 컨텐츠 등급

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>RATING</li> <li> **API 키:**<br/>media.rating</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>TVY, TVG, TVPG, TVMA</li> <li> **설명:**<br/>TV 유해 컨텐츠 가이드라인으로 정의된 등급입니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.rating)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.rating)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>분류</li> <li> **보고서 이름:**<br/>컨텐츠 등급</li> <li> **컨텍스트 데이터:**<br/>(a.media.rating)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.rating)</li> </ul> |

### 작성자

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>ORIGINATOR</li> <li> **API 키:**<br/>media.originator</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&quot;Warner Brothers&quot;, &quot;Sony&quot;, &quot;Disney&quot;</li> <li> **설명:**<br/>컨텐츠 작성자입니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.originator)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.originator)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>분류</li> <li> **보고서 이름:**<br/>작성자</li> <li> **컨텍스트 데이터:**<br/>(a.media.originator)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.originator)</li> </ul> |

### 네트워크

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>NETWORK</li> <li> **API 키:**<br/>media.network</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&quot;Fox&quot;, &quot;Bravo&quot;, &quot;ESPN&quot;</li> <li> **설명:**<br/>네트워크/채널 이름입니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.network)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.network)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>네트워크</li> <li> **컨텍스트 데이터:**<br/>(a.media.network)</li> <li> **데이터 피드:**<br/>videonetwork</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.network)</li> </ul> |

### 표시 유형

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>SHOW_TYPE</li> <li> **API 키:**<br/>media.showType</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&quot;0&quot; = Full episode; &quot;1&quot; = Preview/trailer; &quot;2&quot; = Clip; &quot;3&quot; = Other.</li> <li> **설명:**<br/>0과 3 사이의 정수로 표시되는 컨텐츠의 유형입니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.type)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.type)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>표시 유형</li> <li> **컨텍스트 데이터:**<br/>(a.media.type)</li> <li> **데이터 피드:**<br/>videoshowtype</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.type)</li> </ul> |

### MVPD

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>MVPD</li> <li> **API 키:**<br/>media.pass.mvpd</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&quot;Comcast&quot;, &quot;DirecTV&quot;, &quot;Dish&quot;</li> <li> **설명:**<br/>Adobe 인증을 통해 제공된 MVPD입니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.pass.mvpd)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.pass.<br/>mvpd)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>MVPD</li> <li> **컨텍스트 데이터:**<br/>(a.media.pass.mvpd)</li> <li> **데이터 피드:**<br/>videomvpd</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.pass.mvpd)</li> </ul> |

### 인증됨

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>AUTHORIZED</li> <li> **API 키:**<br/>media.pass.auth</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&quot;TRUE&quot;</li> <li> **설명:**<br/>사용자가 Adobe 인증을 통해 인증되었습니다.<br/>**중요:**설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.pass.auth)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.pass.<br/>auth)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>인증됨</li> <li> **컨텍스트 데이터:**<br/>(a.media.pass.auth)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.pass.auth)</li> </ul> |

### 방송 시간대

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>DAY_PART</li> <li> **API 키:**<br/>media.dayPart</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> </li> <li> **설명:**<br/>컨텐츠가 브로드캐스트 또는 재생되는 시간을 정의하는 속성입니다. 이는 고객이 필요에 따라 모든 값을 설정할 수 있습니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.dayPart)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.dayPart)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>방송 시간대</li> <li> **컨텍스트 데이터:**<br/>(a.media.dayPart)</li> <li> **데이터 피드:**<br/>videodaypart</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.dayPart)</li> </ul> |

### 미디어 피드 유형

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>FEED</li> <li> **API 키:**<br/>media.feed</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&quot;East-HD&quot;, &quot;West-HD&quot;, &quot;East-SD&quot;</li> <li> **설명:**<br/>피드 유형입니다.<br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.feed)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.feed)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/>미디어 피드 유형</li> <li> **컨텍스트 데이터:**<br/>(a.media.feed)</li> <li> **데이터 피드:**<br/>videofeedtype</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.feed)</li> </ul> |

### 아티스트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.artist</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 <br/>[Media Collection 개요](/help/media-collection-api/mc-api-overview.md) 또는 [SDK 다운로드 -버전 2.2](/help/sdk-implement/download-sdks.md)에서 사용할 수 있습니다.  </li> <li> **샘플 값:**<br/>&quot;The Beatles&quot;</li> <li> **설명:**<br/>아티스트의 이름입니다.<br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.artist)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.artist)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/> </li> <li> **컨텍스트 데이터:**<br/>(a.media.artist)</li> <li> **데이터 피드:**<br/>videoaudioartist</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.artist)</li> </ul> |

### 앨범

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.album</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 <br/>[Media Collection 개요](/help/media-collection-api/mc-api-overview.md) 또는 [SDK 다운로드 -버전 2.2](/help/sdk-implement/download-sdks.md)에서 사용할 수 있습니다.  </li> <li> **샘플 값:**<br/>&quot;Revolver&quot;</li> <li> **설명:**<br/>앨범의 이름입니다.<br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.album)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.album)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/> </li> <li> **컨텍스트 데이터:**<br/>(a.media.album)</li> <li> **데이터 피드:**<br/>videoaudioalbum</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.album)</li> </ul> |

### 레이블

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.label</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 <br/>[Media Collection 개요](/help/media-collection-api/mc-api-overview.md) 또는 [SDK 다운로드 -버전 2.2](/help/sdk-implement/download-sdks.md)에서 사용할 수 있습니다.  </li> <li> **샘플 값:**<br/>&quot;Revolver&quot;</li> <li> **설명:**<br/>레코드 레이블의 이름입니다.<br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.label)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.label)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/> </li> <li> **컨텍스트 데이터:**<br/>(a.media.label)</li> <li> **데이터 피드:**<br/>videoaudiolabel</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.label)</li> </ul> |

### Author

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.author</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 <br/>[Media Collection 개요](/help/media-collection-api/mc-api-overview.md) 또는 [SDK 다운로드 -버전 2.2](/help/sdk-implement/download-sdks.md)에서 사용할 수 있습니다.  </li> <li> **샘플 값:**<br/>&quot;John Kennedy Toole&quot;</li> <li> **설명:**<br/>작성자(오디오북)의 이름입니다.<br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.author)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.author)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/> </li> <li> **컨텍스트 데이터:**<br/>(a.media.author)</li> <li> **데이터 피드:**<br/>videoaudioauthor</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.author)</li> </ul> |

### 방송국

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.station</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 <br/>[Media Collection 개요](/help/media-collection-api/mc-api-overview.md) 또는 [SDK 다운로드 -버전 2.2](/help/sdk-implement/download-sdks.md)에서 사용할 수 있습니다.  </li> <li> **샘플 값:**<br/>&quot;NPR&quot;</li> <li> **설명:**<br/>라디오 방송국의 이름/ID입니다.<br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.station)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.station)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/> </li> <li> **컨텍스트 데이터:**<br/>(a.media.station)</li> <li> **데이터 피드:**<br/>videoaudiostation</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.station)</li> </ul> |

### 게시자

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.publisher</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작, 미디어 종료</li> <li> **최소. SDK 버전:** 1.5.7 <br/>[Media Collection 개요](/help/media-collection-api/mc-api-overview.md) 또는 [SDK 다운로드 -버전 2.2](/help/sdk-implement/download-sdks.md)에서 사용할 수 있습니다.  </li> <li> **샘플 값:**<br/>&quot;Random Bauhaus&quot;</li> <li> **설명:**<br/>오디오 컨텐츠 게시자의 이름입니다.<br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.publisher)</li> <li> **하트비트:**<br/>(s:meta:<br/>a.media.publisher)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>히트 시</li> <li> **보고서 이름:**<br/> </li> <li> **컨텍스트 데이터:**<br/>(a.media.publisher)</li> <li> **데이터 피드:**<br/>videoaudiopublisher</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.publisher)</li> </ul> |

## 오디오 및 비디오 지표 {#audio-and-video-metrics}

### 미디어 시작

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 시작</li> <li> **최소. SDK 버전:** Any</li> <li> **샘플 값:**<br/>TRUE</li> <li> **설명:**<br/>미디어에 대한 로드 이벤트입니다. 이 이벤트는 뷰어가_재생&#x200B;_단추를 클릭할 때 발생합니다. 이 이벤트는 프리롤 광고, 버퍼링, 오류 등이 있는 경우에도 계산됩니다.<br/>**중요:**설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.<br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.view)</li> <li> **하트비트:**<br/>(s:event:<br/>type=start)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>미디어 시작</li> <li> **컨텍스트 데이터:**<br/>(a.media.view)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.view)</li> </ul> |

### 컨텐츠 시작

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>TRUE</li> <li> **설명:**<br/>미디어의 첫 번째 프레임이 사용됩니다. 광고, 버퍼링 중에 사용자가 그만두면 &quot;컨텐츠 시작&quot; 이벤트가 일어나지 않습니다.<br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>N/A</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>컨텐츠 시작</li> <li> **컨텍스트 데이터:**<br/>(a.media.play)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.play)</li> </ul> |

### 컨텐츠 완료 {#content-complete}

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>TRUE</li> <li> **설명:**<br/>완성을 위해 관찰된 스트림입니다. 이는 사용자가 반드시 전체 스트림을 보거나 청취했음을 의미하지는 않습니다. 앞으로 건너뛰었을 수도 있습니다. 사용자가 스트림의 끝인 100%에 도달했음을 의미할 뿐입니다.<br/>[세션 종료](quality-parameters.md#session-end)도 참조하십시오.<br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>(s:event:<br/>type=complete)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>컨텐츠 완료</li> <li> **컨텍스트 데이터:**<br/>(a.media.complete)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.complete)</li> </ul> |

### 컨텐츠 체류 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>숫자</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>105</li> <li> **설명:**<br/>기본 컨텐츠에서 재생 유형의 모든 이벤트에 대한 이벤트 기간(초)을 합합니다. 값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다.<br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>N/A</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>컨텐츠 체류 시간</li> <li> **컨텍스트 데이터:**<br/>(a.media.timePlayed)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.timePlayed)</li> </ul> |

### 미디어 사용 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>숫자</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>120</li> <li> **설명:**<br/>기본 컨텐츠와 광고 컨텐츠에서 재생 유형의 모든 이벤트에 대한 이벤트 기간(초)을 합합니다. 값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다.<br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>N/A</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>미디어 사용 시간</li> <li> **컨텍스트 데이터:**<br/>(a.media.totalTimePlayed)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.totalTimePlayed)</li> </ul> |

### 재생된 고유 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>숫자</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>94</li> <li> **설명:**<br/>세션 중에 재생되는 컨텐츠의 고유한 세그먼트의 값(초)입니다. 시청자가 컨텐츠에서 동일한 세그먼트를 여러 번 본다는 다시 찾기 시나리오에서 재생되는 시간은 제외합니다.  값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다.<br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>N/A</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>사용자 지정</li> <li> **컨텍스트 데이터:**<br/>(a.media.uniqueTimePlayed)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.uniqueTimePlayed)</li> </ul> |

### 10% 진행률 마커

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>TRUE</li> <li> **설명:**<br/>플레이헤드가 길이에 따라 컨텐츠의 10% 마커를 전달합니다. 마커는 역방향을 찾으려는 경우에도 한 번만 계산됩니다. 정방향으로 찾는 경우 건너뛴 마커는 계산되지 않습니다.<br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>N/A</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>10% 진행률 마커</li> <li> **컨텍스트 데이터:**<br/>(a.media.progress10)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.progress10)</li> </ul> |

### 25% 진행률 마커

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>TRUE</li> <li> **설명:**<br/>플레이헤드가 컨텐츠 길이에 따라 컨텐츠의 25% 마커를 전달합니다. 마커는 역방향을 찾으려는 경우에도 한 번만 계산됩니다. 정방향으로 찾는 경우 건너뛴 마커는 계산되지 않습니다.<br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>N/A</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>25% 진행률 마커</li> <li> **컨텍스트 데이터:**<br/>(a.media.progress25)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.progress25)</li> </ul> |

### 50% 진행률 마커

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>TRUE</li> <li> **설명:**<br/>플레이헤드가 컨텐츠 길이에 따라 컨텐츠의 50% 마커를 전달합니다. 마커는 역방향을 찾으려는 경우에도 한 번만 계산됩니다. 정방향으로 찾는 경우 건너뛴 마커는 계산되지 않습니다.<br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>N/A</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>50% 진행률 마커</li> <li> **컨텍스트 데이터:**<br/>(a.media.progress50)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.progress50)</li> </ul> |

### 75% 진행률 마커

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/> **N/A** </li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>TRUE</li> <li> **설명:**<br/>플레이헤드가 컨텐츠 길이에 따라 컨텐츠의 75% 마커를 전달합니다. 마커는 역방향을 찾으려는 경우에도 한 번만 계산됩니다. 정방향으로 찾는 경우 건너뛴 마커는 계산되지 않습니다.<br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>N/A</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>75% 진행률 마커</li> <li> **컨텍스트 데이터:**<br/>(a.media.progress75)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.progress75)</li> </ul> |

### 95% 진행률 마커

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>TRUE</li> <li> **설명:**<br/>플레이헤드가 컨텐츠 길이에 따라 컨텐츠의 95% 마커를 전달합니다. 마커는 역방향을 찾으려는 경우에도 한 번만 계산됩니다. 정방향으로 찾는 경우 건너뛴 마커는 계산되지 않습니다.<br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>N/A</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>95% 진행률 마커</li> <li> **컨텍스트 데이터:**<br/>(a.media.progress95)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.progress95)</li> </ul> |

### Average Minute Audience

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>숫자</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>1보다 크거나 같음</li> <li> **설명:**<br/>대상 평균 시간(분) 지표는 한 개의 특정 미디어 항목에 대해 모든 해당 재생 세션의 해당 미디어 길이로 나눈 총 컨텐츠 체류 시간으로 계산됩니다.<br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>N/A</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>대상 평균 시간(분)</li> <li> **컨텍스트 데이터:**<br/>(a.media.averageMinuteAudience)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.averageMinuteAudience)</li> </ul> |

### 마지막 통화 이후 지난 시간(초)

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>숫자</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>600</li> <li> **설명:**<br/>마지막 호출 지표 이후의 시간은 전체 이벤트나 종료 이벤트로 스트림을 닫았다면 0이며, 시간 제한으로 인해 닫히면 보통 600입니다. 이 지표에는 솔루션 변수 및 자동 처리 규칙이 없으므로 저장할 사용자 지정 처리 규칙을 만들어야 합니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>N/A</li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙</li> <li> **예약된 변수:**<br/>N/A</li> <li> **보고서 이름:**<br/>N/A</li> <li> **컨텍스트 데이터:**<br/>(a.media.secondsSinceLastCall)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.secondsSinceLastCall)</li> </ul> |

### 페더레이션된 데이터

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>부울</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>true</li> <li> **설명:**<br/>히트가 페더레이션되면 참으로 설정합니다(즉, 고객이 자체 구현이 아니라 페더레이션된 데이터 공유의 일부로 수신함).</li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>N/A</li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙</li> <li> **예약된 변수:**<br/>N/A</li> <li> **보고서 이름:**<br/>N/A</li> <li> **컨텍스트 데이터:**<br/>(a.media.federated)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.federated)</li> </ul> |

### 예상 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>숫자</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>1 - 19분 재생,<br/>2 - 31분 재생,<br/>3 - 78분 재생.</li> <li> **설명:**<br/>개별 컨텐츠마다 예상되는 비디오 또는 오디오 스트림 수입니다. 이 값은 재생 시간(컨텐츠 + 광고 수) 30분마다 증가합니다. 고객이 보고에 사용할 수 있는 값을 갖도록 고유한 처리 규칙을 만들어야 합니다.<br/><br/>스트림은`ms_s`(또는 totalTimePlayed = Video Total Time)를 기반으로 하여 30분마다 계산되며,<br/>과 비슷합니다. `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>N/A</li> </ul> | <ul> <li> **사용 가능:**<br/>사용자 지정 처리 규칙</li> <li> **예약된 변수:**<br/>N/A</li> <li> **보고서 이름:**<br/>사용자 지정</li> <li> **컨텍스트 데이터:**<br/>(a.media.estimatedStreams)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.estimatedStreams)</li> </ul> |

### 일시 중지된 영향을 받은 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** 1.5.6 </li> <li> **샘플 값:**<br/>TRUE</li> <li> **설명:**<br/>이 값은 참 또는 거짓입니다. 단일 미디어 항목 재생 중 한 번 이상의 일시 정지가 발생한 경우에는 true입니다.<br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>(s:event:<br/>type=pause)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>일시 정지의 영향을 받은 스트림</li> <li> **컨텍스트 데이터:**<br/>(a.media.pause)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.pause)</li> </ul> |

### 일시 중지 이벤트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>숫자</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** 1.5.6 </li> <li> **샘플 값:**<br/>2</li> <li> **설명:**<br/>이 지표는 재생 세션 중에 발생한 일시 중지 기간 횟수로 계산됩니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>(s:event:<br/>type=pause)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>이벤트 일시 중단</li> <li> **컨텍스트 데이터:**<br/>(a.media.pauseCount)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.pauseCount)</li> </ul> |

### 총 일시 중지 기간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>숫자</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** 1.5.6 </li> <li> **샘플 값:**<br/>190</li> <li> **설명:**<br/>일시 정지 유형의 모든 이벤트에 대한 지속 기간(초)을 합합니다. 값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다.<br/> **릴리스 날짜: 2018년 9월 13일** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>N/A</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>총 일시 중단 기간</li> <li> **컨텍스트 데이터:**<br/>(a.media.pauseTime)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.pauseTime)</li> </ul> |

### 컨텐츠 다시 시작

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/> **media.resume** </li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** 1.5.6 </li> <li> **샘플 값:**<br/>TRUE</li> <li> **설명:**<br/>다시 시작은 버퍼, 일시 중지 또는 지연 기간이 30분 이상 지난 후 또는 플레이어가 VideoInfo trackPlay에 이 값을 설정한 경우 다시 시작하는 각 재생에 대해 카운트됩니다.<br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>(s:event:<br/>type=resume)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>컨텐츠 재개</li> <li> **컨텍스트 데이터:**<br/>(a.media.resume)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.resume)</li> </ul> |

### 컨텐츠 세그먼트 보기 수

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨</li> <li> **API 키:**<br/>N/A</li> <li> **유형:**<br/>문자열</li> <li> **전송 시점:**<br/>미디어 닫기</li> <li> **최소. SDK 버전:** Any </li> <li> **샘플 값:**<br/>TRUE</li> <li> **설명:**<br/>기본 컨텐츠 보기 횟수입니다. 본 프레임이 적어도 한 개 있는 경우 컨텐츠 세그먼트 보기가 카운트됩니다.<br/> **중요:** 설정된 경우에만 true일 수 있습니다. 설정되지 않은 경우 값이 반환되지 않습니다. </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A</li> <li> **하트비트:**<br/>N/A</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>이벤트</li> <li> **보고서 이름:**<br/>컨텐츠 세그먼트 보기 수</li> <li> **컨텍스트 데이터:**<br/>(a.media.segmentView)</li> <li> **데이터 피드:**<br/>N/A</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.segmentView)</li> </ul> |

<!--
### Ad Count 

| &nbsp;&nbsp;Implementation&nbsp;&nbsp; | Network&nbsp;Parameters | Reporting |
| --- | --- | --- |
| <ul> <li> **SDK Key:**<br/> N/A </li> <li> **API Key:**<br/> N/A </li> <li> **Type:**<br/> number </li> <li> **Sent with:**<br/> Media Close </li> <li> **Min. SDK Version:** Any </li> <li> **Sample value:**<br/> 2 </li> <li> **Description:**<br/> The number of ads started during the media session.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/A </li> <li> **Heartbeats:**<br/> N/A </li> </ul> | <ul> <li> **Available:**<br/> Use custom processing rule </li> <li> **Reserved Variable:**<br/> N/A </li> <li> **Report Name:**<br/> Custom </li> <li> **Context Data:**<br/> (a.media.adCount) </li> <li> **Data Feed:**<br/> N/A </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.adCount) </li> </ul> |

### Chapter Count 

| &nbsp;&nbsp;Implementation&nbsp;&nbsp; | Network&nbsp;Parameters | Reporting |
| --- | --- | --- |
| <ul> <li> **SDK Key:**<br/> N/A </li> <li> **API Key:**<br/> N/A </li> <li> **Type:**<br/> number </li> <li> **Sent with:**<br/> Media Close </li> <li> **Min. SDK Version:** Any </li> <li> **Sample value:**<br/> 2 </li> <li> **Description:**<br/> The number of chapters started during the media session.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/A </li> <li> **Heartbeats:**<br/> N/A </li> </ul> | <ul> <li> **Available:**<br/> Use custom processing rule </li> <li> **Reserved Variable:**<br/> N/A </li> <li> **Report Name:**<br/> Custom </li> <li> **Context Data:**<br/> (a.media.chapterCount) </li> <li> **Data Feed:**<br/> N/A </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapterCount) </li> </ul> |
-->

## CCPA(California Consumer Privacy Act) 매개 변수 {#ccpa-params}

### 서버 측 전달 거부

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>해당 사항 없음</li> <li> **API 키:**<br/>analytics.optOutServerSideForwarding</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>부울</li> <li> **전송 시점:**<br/>미디어 시작</li> <li> **최소. SDK 버전:** 해당 사항 없음 </li> <li> **샘플 값:**<br/>true</li> <li>**설명:**<br/>최종 사용자가 Adobe Analytics와 다른 Experience Cloud 솔루션(예: Audience Manager) 간에 데이터를 공유하지 않기로 선택한 경우 참으로 설정합니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(opt.dmp)</li> <li> **하트비트:**<br/>(s:meta:cm.ssf)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>방문 시</li> <li> **보고서 이름:**<br/>컨텐츠</li> <li> **컨텍스트 데이터:**<br/>해당 사항 없음</li> <li> **데이터 피드:**<br/>비디오</li> <li> **Audience Manager:**<br/>해당 사항 없음</li> </ul> |

### 공유 옵트아웃

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>해당 사항 없음</li> <li> **API 키:**<br/>analytics.optOutShare</li> <li> **필수:**<br/>아니요</li> <li> **유형:**<br/>부울</li> <li> **전송 시점:**<br/>미디어 시작</li> <li> **최소. SDK 버전:** 해당 사항 없음 </li> <li> **샘플 값:**<br/>true</li> <li>**설명:**<br/>최종 사용자가 데이터를 (예: 다른 Adobe Analytics 클라이언트로) 페더레이션하지 않기로 선택한 경우 참으로 설정합니다.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(opt.oos)</li> <li> **하트비트:**<br/>(s:meta:cm.oos)</li> </ul> | <ul> <li> **사용 가능:**<br/>예</li> <li> **예약된 변수:**<br/>eVar</li> <li> **만료:**<br/>방문 시</li> <li> **보고서 이름:**<br/>컨텐츠</li> <li> **컨텍스트 데이터:**<br/>해당 사항 없음</li> <li> **데이터 피드:**<br/>비디오</li> <li> **Audience Manager:**<br/>해당 사항 없음</li> </ul> |

## 관련 API {#section_Related_APIs}

### createMediaObject API {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig API {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)

