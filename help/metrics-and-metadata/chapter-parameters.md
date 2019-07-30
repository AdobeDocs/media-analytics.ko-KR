---
seo-title: 챕터 매개 변수
title: 챕터 매개 변수
uuid: 2 A 6 B 9247-A 694-46 E 9-98 E 1-424 C 08 C 27 EC 2
translation-type: tm+mt
source-git-commit: af8da9da6cbe36e56f13cd7819f3682522e169bf

---


# 챕터 매개 변수{#chapter-parameters}

이 항목에서는 컨텍스트 데이터 값을 포함하여 Adobe에서 솔루션 변수를 통해 수집하는 챕터 및/또는 세그먼트 데이터의 목록을 제공합니다.

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

>[!IMPORTANT]
>
>아래에 나열된 변수에 대한 분류 이름은 보고/예약 변수 아래에 "분류" 로 설명하지 마십시오.\
>미디어 분류는 미디어 추적에 대해 보고서 세트가 활성화되어 있을 때 정의됩니다. Adobe는 때때로 새 속성을 추가하며, 이러한 경우 고객은 보고서 세트를 다시 활성화하여 새 미디어 속성에 액세스해야 합니다. 업데이트 프로세스 동안 Adobe는 변수의 이름을 검사하여 분류를 사용할지 여부를 결정합니다. 누락된 경우 누락된 항목이 추가됩니다.

## 챕터 메타데이터 {#section_534D3A6BFEB24D1884F80AD6A50BF13C}

### 챕터 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [이름](./chapter-parameters.md#related_apis_section) </li> <li> **API 키:**<br/>media.chapter.friendlyName </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 챕터 시작, 챕터 닫기 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> **샘플 값:**<br/> " The Big Seal Chapter 2 - 데이트 " </li><li> **설명:**<br/>장 및/또는 세그먼트의 이름.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. chapter.<br/>friendlyname) </li> <li> **하트비트:**<br/> (s: 스트림: chapter_ name) </li> </ul> | <ul> <li> **사용 가능:**<br/>기본적으로 작성됨...  </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/>챕터 이름 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. chapter.<br/>friendlyname) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. chapter.<br/>friendlyname) </li> </ul> |

### 챕터 위치

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API 키:**<br/>media.chapter.index </li> <li> **필수:**<br/> SDK: 아니요. API: 예. </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 장 (chapter) 닫기 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> **샘플 값:**<br/> 2 </li><li> **설명:**<br/>컨텐츠 내 챕터의 위치 (인덱스, 정수) 입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. chapter.<br/>position) </li> <li> **하트비트:**<br/> (L: 스트림: chapter_ pos) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/>챕터 위치 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. chapter.<br/>position) </li> <li> **데이터 피드:**<br/> </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. chapter.<br/>position) </li> </ul> |

### 챕터 오프셋

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API 키:**<br/>media.chapter.offset </li> <li> **필수:**<br/> SDK: 아니요. API: 예. </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 장 (chapter) 닫기 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> **샘플 값:**<br/> 58 </li><li> **설명:**<br/>시작 부분에서 컨텐츠 내 챕터의 오프셋 (초) 입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. chapter.<br/>오프셋) </li> <li> **하트비트:**<br/> (L: 스트림: chapter_ offset) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/>챕터 오프셋 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. chapter.<br/>오프셋) </li> <li> **데이터 피드:**<br/> </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. chapter.<br/>오프셋) </li> </ul> |

### 챕터 길이

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/>media.chapter.length </li> <li> **필수:**<br/> SDK: 아니요. API: 예. </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 장 (chapter) 닫기 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> **샘플 값:**<br/> 486 </li><li> **설명:**<br/>The length of the chapter (단위: 초).   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. chapter.<br/>length) </li> <li> **하트비트:**<br/> (L: 스트림: chapter_ length) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/>챕터 길이 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. chapter.<br/>length) </li> <li> **데이터 피드:**<br/> </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. chapter.<br/>length) </li> </ul> |

### 챕터

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 장 (chapter) 닫기 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>The auto-generated ID of the chapter.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. chapter.<br/>이름) </li> <li> **하트비트:**<br/> (s: 스트림: chapter_ id) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>챕터 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. chapter.<br/>이름) </li> <li> **데이터 피드:**<br/>videochapter </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. chapter.<br/>이름) </li> </ul> |

## 챕터 지표 {#section_1C47D6FB1DF343C39CE7A8F724406F33}

### 챕터 시작

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨  </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>챕터 시작 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> **샘플 값:**<br/> true </li><li> **설명:**<br/>장 수가 시작됩니다. **중요:** 이 이벤트가 설정된 경우 TRUE 값만 가능합니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. chapter.<br/>view) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = chapter_ start) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/> 챕터 시작 G </li> <li> **컨텍스트 데이터:**<br/> (a. Media. chapter.<br/>view) </li> <li> **데이터 피드:**<br/>videochapterstart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. chapter.<br/>view) </li> </ul> |

### 챕터 완료

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨  </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **보낸 사람:**<br/> 장 (chapter) 닫기 </li> <li> **최소. SDK 버전:** 1.3</li> <li> **샘플 값:**<br/> true </li><li> **설명:**<br/>장 수가 완료됩니다. **중요:** 이 이벤트가 설정된 경우 TRUE 값만 가능합니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. chapter.<br/>완료됨) </li> <li> **하트비트:**<br/> (s: 이벤트:<br/>type = chapter_ complete) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/> 챕터가 G 완료 </li> <li> **컨텍스트 데이터:**<br/> (a. Media. chapter.<br/>완료됨) </li> <li> **데이터 피드:**<br/>videochaptercomplete </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. chapter.<br/>완료됨) </li> </ul> |

### 챕터 체류 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨  </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>숫자 </li> <li> **보낸 사람:**<br/> 장 (chapter) 닫기 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>The time spent on the chapter. 값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다. <br/>**릴리스 날짜: 2018년 9월 13일**   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. Media. chapter.<br/>timeplayed) </li> <li> **하트비트:**<br/> </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/> 챕터 체류 시간 G </li> <li> **컨텍스트 데이터:**<br/> (a. Media. chapter.<br/>timeplayed) </li> <li> **데이터 피드:**<br/>videochaptertime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. Media. chapter.<br/>timeplayed) </li> </ul> |

## Related APIs {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
