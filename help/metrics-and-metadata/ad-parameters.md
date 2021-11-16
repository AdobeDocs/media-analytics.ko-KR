---
title: 광고 매개 변수
description: “구현, 네트워크 및 광고 비디오 데이터에 대한 변수 보고를 포함하여 광고 매개 변수에 대해 알아봅니다.”
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
exl-id: 949e86cb-d265-4836-8825-a06b87203b15
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: f296b2549bb49162d735f29718057b3b1bbec231
workflow-type: ht
source-wordcount: '1927'
ht-degree: 100%

---

# 광고 매개 변수{#ad-parameters}

이 항목에서는 컨텍스트 데이터 값을 포함하여 Adobe에서 솔루션 변수를 통해 수집하는 비디오 광고 데이터의 목록을 제공합니다.

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
>보고/예약 변수 아래에 &quot;분류&quot;로 설명되어 있는 변수의
>분류 이름을 변경하지 마십시오.
>미디어 분류는 보고서 세트가 미디어 추적에 대해 활성화될 때
>정의됩니다. Adobe는 수시로 새로운 속성을 추가하며, 이런 경우
>고객이 보고서 세트를 다시 활성화하여 새 미디어 속성에
>액세스해야 합니다. 업데이트 프로세스 중에 Adobe는 변수의 이름을 확인하여
>분류를 사용할지 여부를 결정합니다. 누락된 항목이
>있을 경우 Adobe가 다시 추가합니다.

## 광고 비디오 데이터 {#ad-video-data}

### 광고 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/> media.ad.id </li> <li> **필수:**<br/>&#x200B;예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>&#x200B;광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두  </li> <li> **샘플 값:**<br/> &quot;2125&quot; </li><li> **설명:**<br/>&#x200B;광고 ID입니다. (모든 정수 및/또는 문자 조합)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>name) </li> <li> **하트비트:**<br/> (s:asset:ad_id) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/> eVar </li> <li> **만료:**<br/>&#x200B;방문 시 </li> <li> **보고서 이름:**<br/>&#x200B;광고 </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.<br/>name) </li> <li> **데이터 피드:**<br/> videoad </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.name) </li> <li> **XDM 필드 패스:**<br/> advertising.adAssetReference.@ID </li> </ul> |



### Pod의 광고 위치

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/> media.ad.podPosition </li> <li> **필수:**<br/>&#x200B;예 </li> <li> **유형:**<br/>&#x200B;숫자 </li> <li> **전송 시점:**<br/>&#x200B;광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 1 </li><li> **설명:**<br/>&#x200B;상위 광고 브레이크 내에 있는 광고의 위치(색인)입니다. 첫 번째 광고에는 색인 0, 두 번째 광고에 색인 1 등이 있습니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **하트비트:**<br/> (s:asset:pod_position) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/> eVar </li> <li> **만료:**<br/>&#x200B;히트 시 </li> <li> **보고서 이름:**<br/> Pod의 광고 위치의 </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **데이터 피드:**<br/> videoadinpod </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podPosition) </li> <li> **XDM 필드 패스:**<br/> advertising.adAssetViewDetails.index </li> </ul> |



### 광고 길이

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/> media.ad.length </li> <li> **필수:**<br/>&#x200B;예 </li> <li> **유형:**<br/>&#x200B;숫자 </li> <li> **전송 시점:**<br/>&#x200B;광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.1 </li> <li> **샘플 값:**<br/> &quot;15&quot;  </li><li> **설명:**<br/>&#x200B;동영상 광고의 길이(초)입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>length) </li> <li> **하트비트:**<br/> (l:asset:ad_length) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/> eVar 및 분류 </li> <li> **만료:**<br/>&#x200B;히트 시 </li> <li> **보고서 이름:**<br/>&#x200B;광고 길이 및 광고 길이(변수) </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.<br/>length) </li> <li> **데이터 피드:**<br/> videoadlength </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.length) </li> <li> **XDM 필드 패스:**<br/> advertising.adAssetReference.xmpDM:duration </li> </ul> |



### 광고 플레이어 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/> media.ad.playerName </li> <li> **필수:**<br/>&#x200B;예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>&#x200B;광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> &quot;Freewheel&quot; </li><li> **설명:**<br/>&#x200B;광고 렌더링을 담당하는 플레이어의 이름입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>playerName) </li> <li> **하트비트:**<br/> (s:sp:player_name) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/> eVar </li> <li> **만료:**<br/>&#x200B;히트 시 </li> <li> **보고서 이름:**<br/>&#x200B;광고 플레이어 이름 </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.<br/>playerName) </li> <li> **데이터 피드:**<br/> videoadplayername </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.playerName) </li> <li> **XDM 필드 패스:**<br/> advertising.adAssetViewDetails.playerName </li> </ul> |



### 광고 브레이크 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/> media.ad.podFriendlyName </li> <li> **필수:**<br/> SDK: 예, API: 아니요. </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>&#x200B;광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> &quot;프리롤&quot; </li><li> **설명:**<br/>&#x200B;친숙한 광고 브레이크 이름입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **하트비트:**<br/> (s:asset:pod_name) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/>&#x200B;분류 </li> <li> **보고서 이름:**<br/> Pod 이름 </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **데이터 피드:**<br/>&#x200B;해당 사항 없음 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> <li> **XDM 필드 패스:**<br/> advertising.adAssetViewDetails.adBreak.dc:title </li> </ul> |



### 광고 브레이크 색인

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/> media.ad.podPosition </li> <li> **필수:**<br/>&#x200B;예 </li> <li> **유형:**<br/>&#x200B;숫자 </li> <li> **전송 시점:**<br/> </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 1 </li><li> **설명:**<br/>&#x200B;콘텐츠 내에 있는 광고 브레이크 색인(1부터 시작)입니다. 속성은 Media SDK에서 Pod ID를 생성하는 데&#x200B;**에만** 사용됩니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **하트비트:**<br/> </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;아니요 </li> <li> **예약된 변수:**<br/>&#x200B;해당 사항 없음 </li> <li> **보고서 이름:**<br/>&#x200B;해당 사항 없음 </li> <li> **컨텍스트 데이터:**<br/> </li> <li> **데이터 피드:**<br/>&#x200B;해당 사항 없음 </li> <li> **Audience Manager:**<br/> </li> <li> **XDM 필드 패스:**<br/> advertising.adAssetViewDetails.index </li> </ul> |



### 광고 브레이크 위치

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/> media.ad.podSecond </li> <li> **필수:**<br/>&#x200B;예 </li> <li> **유형:**<br/>&#x200B;숫자 </li> <li> **전송 시점:**<br/>&#x200B;광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 90 </li><li> **설명:**<br/>&#x200B;콘텐츠 내부의 광고 브레이크 오프셋(초)입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **하트비트:**<br/> (l:asset:pod_offset) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/>&#x200B;분류 </li> <li> **보고서 이름:**<br/> Pod 위치 </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **데이터 피드:**<br/>&#x200B;해당 사항 없음 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podSecond) </li> <li> **XDM 필드 패스:**<br/> advertising.adAssetViewDetails.adBreak.offset </li> </ul> |



### 광고 브레이크 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>&#x200B;자동으로 설정됨 </li> <li> **API 키:**<br/>&#x200B;해당 사항 없음 </li> <li> **필수:**<br/>&#x200B;예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>&#x200B;광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>pod) </li> <li> **하트비트:**<br/> (s:asset:pod_id) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/> eVar </li> <li> **만료:**<br/>&#x200B;히트 시 </li> <li> **보고서 이름:**<br/>&#x200B;광고 Pod </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.<br/>pod) </li> <li> **데이터 피드:**<br/> videoadpod </li> <li> **Audience Manager:**<br/> </li> <li> **XDM 필드 패스:**<br/> advertising.adAssetViewDetails.adBreak.@ID </li> </ul> |



### 광고 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/> media.ad.name </li> <li> **필수:**<br/>&#x200B;아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>&#x200B;광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.1 </li> <li> **샘플 값:**<br/> &quot;Ford F-150&quot; </li><li> **설명:**<br/>&#x200B;친숙한 광고 이름입니다.  보고 시 &quot;광고 이름&quot;은 분류이고, &quot;광고 이름(변수)&quot;은 eVar입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **하트비트:**<br/> (s:asset:ad_name) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/> eVar 및 분류 </li> <li> **만료:**<br/>&#x200B;히트 시 </li> <li> **보고서 이름:**<br/>&#x200B;광고 이름 및 광고 이름(변수) </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **데이터 피드:**<br/>&#x200B;해당 사항 없음 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.friendlyName) </li> <li> **XDM 필드 패스:**<br/> advertising.adAssetReference.dc:title </li> </ul> |



## 표준 광고 메타데이터 {#standard-ad-metadata}

### 광고주

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> ADVERTISER </li> <li> **API 키:**<br/> media.ad.advertiser </li> <li> **필수:**<br/>&#x200B;아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>&#x200B;광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>&#x200B;광고에서 다루고 있는 제품의 회사/브랜드입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>advertiser) </li> <li> **하트비트:**<br/> (s:meta:<br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/> eVar </li> <li> **만료:**<br/>&#x200B;히트 시 </li> <li> **보고서 이름:**<br/> <i>광고주 </i> </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.<br/>advertiser) </li> <li> **데이터 피드:**<br/> videoadvertiser </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.advertiser) </li> <li> **XDM 필드 패스:**<br/> advertising.adAssetReference.advertiser </li> </ul> |



### 캠페인 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> CAMPAIGN_ID </li> <li> **API 키:**<br/> media.ad.campaignId </li> <li> **필수:**<br/>&#x200B;아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>&#x200B;광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&#x200B;정수 또는 이름(문자열).  </li><li> **설명:**<br/>&#x200B;광고 캠페인의 ID입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>campaign) </li> <li> **하트비트:**<br/> (s:meta:<br/>a.media.ad.campaign) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/> eVar </li> <li> **만료:**<br/>&#x200B;히트 시 </li> <li> **보고서 이름:**<br/> <i>캠페인 ID </i> </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.<br/>campaign) </li> <li> **데이터 피드:**<br/> videocampaign </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.campaign) </li> <li> **XDM 필드 패스:**<br/> advertising.adAssetReference.campaign </li> </ul> |



### 광고 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> CREATIVE_ID </li> <li> **API 키:**<br/> media.ad.creativeId </li> <li> **필수:**<br/>&#x200B;아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>&#x200B;광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/>&#x200B;정수 또는 이름(문자열).  </li><li> **설명:**<br/>&#x200B;광고 문안의 ID입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creative) </li> <li> **하트비트:**<br/> (s:meta:<br/>a.media.ad.creative) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/> eVar </li> <li> **만료:**<br/>&#x200B;히트 시 </li> <li> **보고서 이름:**<br/> <i>광고 ID </i> </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.<br/>creative) </li> <li> **데이터 피드:**<br/> adclassificationcreative </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creative) </li> <li> **XDM 필드 패스:**<br/> advertising.adAssetReference.creativeID </li> </ul> |



### 사이트 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> SITE_ID </li> <li> **API 키:**<br/> media.ad.siteId </li> <li> **필수:**<br/>&#x200B;아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>&#x200B;광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>&#x200B;광고 사이트의 ID입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>없습니다) </li> <li> **하트비트:**<br/> (s:meta:<br/>a.media.ad.site) </li> </ul> | <ul> <li> **사용 가능:**<br/> <i>사용자 지정 처리 규칙 사용 </i> </li> <li> **예약된 변수:**<br/> eVar </li> <li> **만료:**<br/>&#x200B;히트 시 </li> <li> **보고서 이름:**<br/> 사용자 지정 </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.<br/>없습니다) </li> <li> **데이터 피드:**<br/>&#x200B;해당 사항 없음 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.site) </li> <li> **XDM 필드 패스:**<br/> advertising.adAssetReference.siteID </li> </ul> |



### 광고 URL

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> CREATIVE_URL </li> <li> **API 키:**<br/> media.ad.creativeURL </li> <li> **필수:**<br/>&#x200B;아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>&#x200B;광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> </li><li> **Description:**<br/>&#x200B;광고 문안의 URL입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **하트비트:**<br/> (s:meta:<br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **사용 가능:**<br/> <i>사용자 지정 처리 규칙 사용 </i> </li> <li> **예약된 변수:**<br/> eVar </li> <li> **만료:**<br/>&#x200B;히트 시 </li> <li> **보고서 이름:**<br/> 사용자 지정 </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **데이터 피드:**<br/>&#x200B;해당 사항 없음 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creativeURL) </li> <li> **XDM 필드 패스:**<br/> advertising.adAssetReference.creativeURL </li> </ul> |



### 게재위치 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> PLACEMENT_ID </li> <li> **API 키:**<br/> media.ad.placementId </li> <li> **필수:**<br/>&#x200B;아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>&#x200B;광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>&#x200B;광고 배치 ID입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>placement) </li> <li> **하트비트:**<br/> (s:meta:<br/>a.media.ad.placement) </li> </ul> | <ul> <li> **사용 가능:**<br/> <i>사용자 지정 처리 규칙 사용 </i> </li> <li> **예약된 변수:**<br/> eVar </li> <li> **만료:**<br/>&#x200B;히트 시 </li> <li> **보고서 이름:**<br/> 사용자 지정 </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.<br/>placement) </li> <li> **데이터 피드:**<br/>&#x200B;해당 사항 없음 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.placement) </li> <li> **XDM 필드 패스:**<br/> advertising.adAssetReference.placementID </li> </ul> |




## 광고 지표 {#ad-metrics}

### 광고 시작

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>&#x200B;자동으로 설정됨 </li> <li> **API 키:**<br/>&#x200B;해당 사항 없음 </li> <li> **필수:**<br/>&#x200B;예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>&#x200B;광고 시작 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> TRUE </li><li> **설명:**<br/>&#x200B;비디오 광고 시작 수입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>view) </li> <li> **하트비트:**<br/>  (s:event:type=start)<br/> (s:asset:type=ad) </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/>&#x200B;이벤트 </li> <li> **보고서 이름:**<br/>&#x200B;광고 시작 </li> <li> **데이터 피드:**<br/>&#x200B;해당 사항 없음 </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.<br/>view) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.view) </li> <li> **XDM 필드 패스:**<br/> advertising.starts.value > 0 => “TRUE” </li> </ul> |



### 광고 완료

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>&#x200B;자동으로 설정됨 </li> <li> **API 키:**<br/>&#x200B;해당 사항 없음 </li> <li> **필수:**<br/>&#x200B;예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>&#x200B;광고 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> TRUE </li><li> **설명:**<br/>&#x200B;비디오 광고 완료 수입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>complete) </li> <li> **하트비트:**<br/> (s:event:type=complete)<br/> (s:asset:type=ad)  </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/>&#x200B;이벤트 </li> <li> **보고서 이름:**<br/>&#x200B;광고 완료 </li> <li> **데이터 피드:**<br/>&#x200B;해당 사항 없음 </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.<br/>complete) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.complete) </li> <li> **XDM 필드 패스:**<br/> advertising.completes.value > 0 => “TRUE” </li> </ul> |



### 광고 체류 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>&#x200B;자동으로 설정됨 </li> <li> **API 키:**<br/>&#x200B;해당 사항 없음 </li> <li> **필수:**<br/>&#x200B;예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>&#x200B;광고 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 15 </li><li> **설명:**<br/>&#x200B;광고를 시청하는 데 걸린 총 시간(즉, 재생되는 시간(초))입니다.  Analysis Workspace 및 Reports &amp; Analytics에서는 값이 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다.  <br/>**릴리스 날짜: 2018년 9월 13일**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **하트비트:**<br/> </li> </ul> | <ul> <li> **사용 가능:**<br/>&#x200B;예 </li> <li> **예약된 변수:**<br/>&#x200B;이벤트 </li> <li> **보고서 이름:**<br/>&#x200B;광고 체류 시간 </li> <li> **데이터 피드:**<br/>&#x200B;해당 사항 없음 </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.timePlayed) </li> <li> **XDM 필드 패스:**<br/> advertising.timePlayed.value </li> </ul> |



## 관련 API {#section_Related_APIs}

### createAdObject APIs:

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### createAdBreakObject APIs:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### MediaHeartbeatConfig API:

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)
