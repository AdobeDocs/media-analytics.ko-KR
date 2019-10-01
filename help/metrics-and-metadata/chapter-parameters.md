---
seo-title: 챕터 매개 변수
title: 챕터 매개 변수
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 4a14e2faae6401a3f885eb5e341c1344d7f1e94d

---


# 챕터 매개 변수{#chapter-parameters}

이 항목에서는 컨텍스트 데이터 값을 포함하여 Adobe에서 솔루션 변수를 통해 수집하는 챕터 및/또는 세그먼트 데이터의 목록을 제공합니다.

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

>[!IMPORTANT]
>
>보고/예약 변수에 "분류"로 설명된 아래 나열된 변수에 대한 분류 이름을 변경하지 마십시오.\
>The media classifications are defined when a report suite is enabled for media tracking. Adobe는 수시로 새 속성을 추가하고, 이 경우 고객은 보고서 세트를 다시 활성화하여 새로운 미디어 속성에 액세스해야 합니다. 업데이트 프로세스 동안 Adobe는 변수의 이름을 확인하여 분류를 사용할지 여부를 결정합니다. 누락된 항목이 있으면 Adobe는 누락된 항목을 다시 추가합니다.

## 챕터 메타데이터 {#section_534D3A6BFEB24D1884F80AD6A50BF13C}

### 챕터 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [이름](./chapter-parameters.md#related_apis_section) </li> <li> **API 키:**<br/>media.chapter.friendlyName </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:장 시작, 장 종료 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> ****<br/> Sample Value: "The Big Bang Chapter 2 - Dating" </li><li> **Description:**<br/>The name of the chapter and/or segment.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>friendlyName) </li> <li> ****<br/> 하트비트:(s:stream:chapter_name) </li> </ul> | <ul> <li> **사용 가능:**<br/>기본적으로 작성됨...  </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/>챕터 이름 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.chapter.<br/>friendlyName) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter.<br/>friendlyName) </li> </ul> |

### 챕터 위치

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API 키:**<br/>media.chapter.index </li> <li> ****<br/> 필수:SDK:아니오;API:네 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:장 닫기 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> ****<br/> 샘플 값:2 </li><li> **설명:**<br/>컨텐츠 내의 장의 위치(인덱스, 정수)입니다.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>position) </li> <li> **Heartbeat:**<br/> (l:stream:chapter_pos) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/>챕터 위치 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.chapter.<br/>position) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>position) </li> </ul> |

### 챕터 오프셋

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API 키:**<br/>media.chapter.offset </li> <li> ****<br/> 필수:SDK:아니오;API:네 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:장 닫기 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> ****<br/> 샘플 값:58년 </li><li> **설명:**<br/>컨텐츠 내 장(초)의 오프셋을 시작부터 시작합니다.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>오프셋) </li> <li> ****<br/> 하트비트:(l:stream:chapter_offset) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/>챕터 오프셋 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.chapter.<br/>오프셋) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>오프셋) </li> </ul> |

### 챕터 길이

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.chapter.length </li> <li> ****<br/> 필수:SDK:아니오;API:네 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:장 닫기 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> ****<br/> 샘플 값:486년 </li><li> **설명:**<br/>장 길이(초)입니다.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>length) </li> <li> ****<br/> 하트비트:(l:stream:chapter_length) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/>챕터 길이 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.chapter.<br/>length) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter.<br/>length) </li> </ul> |

### 챕터

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **Sent with:**<br/> Chapter Close </li> <li> **최소. SDK 버전:** 1.3 </li> <li> **Sample Value:**<br/> </li><li> **Description:**<br/>The auto-generated ID of the chapter.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>이름) </li> <li> **Heartbeat:**<br/> (s:stream:chapter_id) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>챕터 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.chapter.<br/>이름) </li> <li> **데이터 피드:**<br/>videochapter </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>이름) </li> </ul> |

## 챕터 지표 {#section_1C47D6FB1DF343C39CE7A8F724406F33}

### 챕터 시작

|   구현   | Network Parameters | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨  </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>챕터 시작 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> ****<br/> 샘플 값:TRUE </li><li> **설명:**<br/>장 시작 횟수입니다.  **중요:** 이 이벤트가 설정된 경우 TRUE 값만 가능합니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>view) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=chapter_start) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **Report Name:**<br/> Chapter Starts g </li> <li> ****<br/> 컨텍스트 데이터:(a.media.chapter.<br/>view) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter.<br/>view) </li> </ul> |

### 챕터 완료

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨  </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> ****<br/> 전송 대상:장 닫기 </li> <li> **최소. SDK 버전:** 1.3</li> <li> ****<br/> 샘플 값:TRUE </li><li> **Description:**<br/>The number of chapter completes.  **중요:** 이 이벤트가 설정된 경우 TRUE 값만 가능합니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>완료됨) </li> <li> ****<br/> 하트비트:(s:event:<br/>type=chapter_complete) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> ****<br/> 보고서 이름:장 완료 g </li> <li> ****<br/> Context Data: (a.media.chapter.<br/>완료됨) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter.<br/>완료됨) </li> </ul> |

### 챕터 체류 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨  </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>숫자 </li> <li> ****<br/> 전송 대상:장 닫기 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> **Sample Value:**<br/> </li><li> **Description:**<br/>The time spent on the chapter.  값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다. <br/>**릴리스 날짜: 2018년 9월 13일**   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>timePlayed) </li> <li> **하트비트:**<br/> </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **Report Name:**<br/> Chapter Time Spent g </li> <li> ****<br/> 컨텍스트 데이터:(a.media.chapter.<br/>timePlayed) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>timePlayed) </li> </ul> |

## 관련 API {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
