---
title: 챕터 매개 변수
description: “구현, 네트워크 및 보고에 대한 챕터 매개 변수에 대해 알아봅니다.”
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: 73da3e52-9498-478e-bfd7-8ff6c8e6bfc5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 771cffe923af41d10cb6589d85cf984c43480c29
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 94%

---

# 챕터 매개 변수{#chapter-parameters}

이 항목에서는 컨텍스트 데이터 값을 포함하여 Adobe에서 솔루션 변수를 통해 수집하는 챕터 및/또는 세그먼트 데이터의 목록을 제공합니다.

테이블 데이터 설명:

* **구현:** 구현 값 및 요구 사항에 대한 정보
   * *키* - 앱에서 수동으로 설정하거나 Adobe Media SDK에 의해 자동으로 설정된 변수.
   * *필수* - 기본 비디오 추적에 매개 변수가 필요한지 여부를 나타냅니다.
   * *유형* - 설정할 변수의 유형을 문자열 또는 숫자로 지정합니다.
   * *전송 시점* - 데이터가 전송되는 시점을 나타냅니다. *미디어 시작*&#x200B;은 미디어 시작 시 분석 호출이 전송되고, *광고 시작*&#x200B;은 광고 시작 시 분석 호출이 전송됩니다. *닫기* 호출은 미디어 세션 종료 시 또는 광고, 챕터 종료 시 하트비트 서버에서 Analytics 서버로 컴파일된 분석 호출이 직접 전송됩니다. 닫기 호출은 네트워크 패킷 호출에 사용할 수 없습니다.
   * *최소. SDK 버전* - 매개 변수에 액세스하는 데 필요한 SDK 버전을 나타냅니다.
   * *샘플 값* - 일반적인 변수 사용의 예를 제공합니다.
* **네트워크 매개 변수:** Adobe Analytics 또는 하트비트 서버에 전달되는 값을 표시합니다. 이 열에는 Adobe Media SDK에서 생성한 네트워크 호출에 표시되는 매개 변수의 이름이 표시됩니다.
* **보고:** 비디오 데이터를 보고 분석하는 방법에 대한 정보입니다.
   * *사용 가능* - 데이터가 기본적으로(*예*) 보고 시 사용할 수 있는지 아니면 사용자 지정 설정(*사용자 지정*)을 필요로 하는지 여부를 지정합니다.
   * *예약된 변수* - 데이터가 예약된 변수에 이벤트, eVar, prop 또는 분류로 캡처되는지 여부를 나타냅니다.
   * *보고서 이름* - 변수에 대한 Adobe Analytics 보고서의 이름
   * *컨텍스트 데이터* - 보고 서버에 전달되고 처리 규칙에 사용되는 Adobe Analytics 컨텍스트 데이터의 이름
   * *데이터 피드* - 클릭스트림 또는 라이브 스트림 데이터 피드에 있는 변수의 열 이름
   * *Audience Manager* - Adobe Audience Manager에 있는 트레이트 이름

>[!IMPORTANT]
>
>보고/예약 변수 아래에 &quot;분류&quot;로 설명되어 있는 변수의 분류 이름을 변경하지 마십시오.\
>미디어 분류는 보고서 세트가 미디어 추적에 사용될 때 정의됩니다. Adobe는 수시로 새 속성을 추가하며, 이 경우 고객이 보고서 세트를 다시 활성화하여 새로운 미디어 속성에 액세스해야 합니다. 업데이트 프로세스 중에 Adobe는 변수의 이름을 확인하여 분류를 사용할지 여부를 결정합니다. 누락된 항목이 있을 경우 Adobe가 다시 추가합니다.

## 챕터 메타데이터 {#chapter-metadata}

### 챕터 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 키:**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **API 키:**<br/> media.chapter.friendlyName </li> <li> **필수:**<br/>&#x200B;아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/> 챕터 시작, 챕터 닫기 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> **샘플 값:**<br/> &quot;The Big Bang Chapter 2 - Dating&quot; </li><li> **설명:**<br/>&#x200B;챕터 및/또는 세그먼트의 이름입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **하트비트:**<br/> (s:stream:chapter_name) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;기본적으로 작성됨...  </li> <li> **예약된 변수:**<br/>&#x200B;분류 </li> <li> **보고서 이름:**<br/>&#x200B;챕터 이름 </li> <li> **컨텍스트 데이터:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **데이터 피드:**<br/>&#x200B;해당 사항 없음 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>friendlyName) </li> <li> **XDM 필드 패스:**<br/> media.mediaTimed.mediaChapter.chapterAssetReference.dc:title </li> <li> **컬렉션 XDM 필드 경로:**<br/> mediaCollection.chapterDetails.friendlyName </li> <li> **보고 XDM 필드 경로:**<br/> mediaReporting.chapterDetails.friendlyName </li> </ul> |

### 챕터 위치

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 키:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API 키:**<br/> media.chapter.index </li> <li> **필수:**<br/> SDK:아니요. API: 예. </li> <li> **유형:**<br/>&#x200B;숫자 </li> <li> **전송 시점:**<br/> 챕터 닫기 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> **샘플 값:**<br/> 2 </li><li> **설명:**<br/>&#x200B;콘텐츠 내에서 챕터의 위치(색인, 정수)입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>position) </li> <li> **하트비트:**<br/> (l:stream:chapter_pos) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/>&#x200B;분류 </li> <li> **보고서 이름:**<br/>&#x200B;챕터 위치 </li> <li> **컨텍스트 데이터:**<br/> (a.media.chapter.<br/>position) </li> <li> **데이터 피드:**<br/>&#x200B;해당 사항 없음 </li> <li> **Audience Manager:**<br/> (c_contextdata).<br/>a.media.chapter.<br/>position) </li> <li> **XDM 필드 패스:**<br/> media.mediaTimed.mediaChapter.chapterAssetViewDetails.index </li> <li> **컬렉션 XDM 필드 경로:**<br/> mediaCollection.chapterDetails.index </li> <li> **보고 XDM 필드 경로:**<br/> mediaReporting.chapterDetails.index </li> </ul> |

### 챕터 오프셋

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 키:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API 키:**<br/> media.chapter.offset </li> <li> **필수:**<br/> SDK: 아니요. API: 예. </li> <li> **유형:**<br/>&#x200B;숫자 </li> <li> **전송 시점:**<br/> 챕터 닫기 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> **샘플 값:**<br/> 58 </li><li> **설명:**<br/>&#x200B;처음부터 콘텐츠 내에 있는 챕터의 오프셋(초)입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>offset) </li> <li> **하트비트:**<br/> (l:stream:chapter_offset) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/>&#x200B;분류 </li> <li> **보고서 이름:**<br/>&#x200B;챕터 오프셋 </li> <li> **컨텍스트 데이터:**<br/> (a.media.chapter.<br/>offset) </li> <li> **데이터 피드:**<br/>&#x200B;해당 사항 없음 </li> <li> **Audience Manager:**<br/> (c_contextdata).<br/>a.media.chapter.<br/>offset) </li> <li> **XDM 필드 패스:**<br/> media.mediaTimed.mediaChapter.chapterAssetViewDetails.offset </li> <li> **컬렉션 XDM 필드 경로:**<br/> mediaCollection.chapterDetails.offset </li> <li> **보고 XDM 필드 경로:**<br/> mediaReporting.chapterDetails.offset </li> </ul> |

### 챕터 길이

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 키:**<br/> </li> <li> **API 키:**<br/> media.chapter.length </li> <li> **필수:**<br/> SDK:아니요. API: 예. </li> <li> **유형:**<br/>&#x200B;숫자 </li> <li> **전송 시점:**<br/> 챕터 닫기 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> **샘플 값:**<br/> 486 </li><li> **설명:**<br/>&#x200B;챕터의 길이(초)입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>length) </li> <li> **하트비트:**<br/> (l:stream:chapter_length) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/>&#x200B;분류 </li> <li> **보고서 이름:**<br/>&#x200B;챕터 길이 </li> <li> **컨텍스트 데이터:**<br/> (a.media.chapter.<br/>length) </li> <li> **데이터 피드:**<br/>&#x200B;해당 사항 없음 </li> <li> **Audience Manager:**<br/> (c_contextdata).<br/>a.media.chapter.<br/>length) </li> <li> **XDM 필드 패스:**<br/> media.mediaTimed.mediaChapter.chapterAssetReference.xmpDM:duration </li> <li> **컬렉션 XDM 필드 경로:**<br/> mediaCollection.chapterDetails.length </li> <li> **보고 XDM 필드 경로:**<br/> mediaReporting.chapterDetails.length </li> </ul> |

### 챕터

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 키:**<br/>&#x200B;자동으로 설정됨 </li> <li> **API 키:**<br/>&#x200B;해당 사항 없음 </li> <li> **필수:**<br/>&#x200B;아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/> 챕터 닫기 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>&#x200B;자동으로 생성된 챕터의 ID입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>name) </li> <li> **하트비트:**<br/> (s:stream:chapter_id) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/> eVar </li> <li> **만료:**<br/>&#x200B;히트 시 </li> <li> **보고서 이름:**<br/>&#x200B;챕터 </li> <li> **컨텍스트 데이터:**<br/> (a.media.chapter.<br/>name) </li> <li> **데이터 피드:**<br/> videochapter </li> <li> **Audience Manager:**<br/> (c_contextdata).<br/>a.media.chapter.<br/>이름) </li> <li> **XDM 필드 패스:**<br/> media.mediaTimed.mediaChapter.chapterAssetReference.@ID </li> <li> **보고 XDM 필드 경로:**<br/> mediaReporting.chapterDetails.chapterID </li> </ul> |

## 챕터 지표 {#chapter-Metrics}

### 챕터 시작

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 키:**<br/>&#x200B;자동으로 설정됨  </li> <li> **API 키:**<br/>&#x200B;해당 사항 없음 </li> <li> **필수:**<br/>&#x200B;예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>&#x200B;챕터 시작 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> **샘플 값:**<br/> TRUE </li><li> **설명:**<br/>&#x200B;챕터 시작 횟수입니다.  **중요:** 이 이벤트가 설정된 경우 TRUE 값만 가능합니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>view) </li> <li> **하트비트:**<br/> (s:event:<br/>type=chapter_start) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/>&#x200B;이벤트 </li> <li> **보고서 이름:**<br/> 챕터 시작</li> <li> **컨텍스트 데이터:**<br/> (a.media.chapter.<br/>view) </li> <li> **데이터 피드:**<br/>&#x200B;해당 사항 없음 </li> <li> **Audience Manager:**<br/> (c_contextdata).<br/>a.media.chapter.<br/>view) </li> <li> **XDM 필드 패스:**<br/> media.mediaTimed.chapterCount.value > 0 => “TRUE” </li> <li> **보고 XDM 필드 경로:**<br/> mediaReporting.chapterDetails.isStarted </li> </ul> |

### 챕터 완료

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 키:**<br/>&#x200B;자동으로 설정됨  </li> <li> **API 키:**<br/>&#x200B;해당 사항 없음 </li> <li> **필수:**<br/>&#x200B;예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/> 챕터 닫기 </li> <li> **최소. SDK 버전:** 1.3</li> <li> **샘플 값:**<br/> TRUE </li><li> **설명:**<br/>&#x200B;챕터 완료 횟수입니다.  **중요:** 이 이벤트가 설정된 경우 TRUE 값만 가능합니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>complete) </li> <li> **하트비트:**<br/> (s:event:<br/>type=chapter_complete) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/>&#x200B;이벤트 </li> <li> **보고서 이름:**<br/> 챕터 완료</li> <li> **컨텍스트 데이터:**<br/> (a.media.chapter.<br/>complete) </li> <li> **데이터 피드:**<br/>&#x200B;해당 사항 없음 </li> <li> **Audience Manager:**<br/> (c_contextdata).<br/>a.media.chapter.<br/>complete) </li> <li> **XDM 필드 패스:**<br/> media.mediaTimed.mediaChapter.completes.value </li> <li> **보고 XDM 필드 경로:**<br/> mediaReporting.chapterDetails.isCompleted </li> </ul> |

### 챕터 체류 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 키:**<br/>&#x200B;자동으로 설정됨  </li> <li> **API 키:**<br/>&#x200B;해당 사항 없음 </li> <li> **필수:**<br/>&#x200B;예 </li> <li> **유형:**<br/>&#x200B;숫자 </li> <li> **전송 시점:**<br/> 챕터 닫기 </li> <li> **최소. SDK 버전:** 1.3 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>&#x200B;챕터에서 보낸 시간입니다.  Analysis Workspace 및 Reports &amp; Analytics에서는 값이 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다. <br/>**릴리스 날짜: 2018년 9월 13일**   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **하트비트:**<br/> </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/>&#x200B;이벤트 </li> <li> **보고서 이름:**<br/> 챕터 체류 시간</li> <li> **컨텍스트 데이터:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **데이터 피드:**<br/>&#x200B;해당 사항 없음 </li> <li> **Audience Manager:**<br/> (c_contextdata).<br/>a.media.chapter.<br/>timePlayed) </li> <li> **XDM 필드 패스:**<br/> media.mediaTimed.mediaChapter.timePlayed.value </li> <li> **보고 XDM 필드 경로:**<br/> mediaReporting.chapterDetails.timePlayed </li> </ul> |

## 관련 API {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
