---
seo-title: 광고 매개 변수
title: 광고 매개 변수
uuid: 92 CD 7 F 97-BB 5 A -4 DE 6-8946-453 D 30271 D 0 F
translation-type: tm+mt
source-git-commit: 180eafdfc536039820ade0b52e5c55f874719d8e

---


# 광고 매개 변수{#ad-parameters}

이 항목에서는 컨텍스트 데이터 값을 포함하여 Adobe에서 솔루션 변수를 통해 수집하는 비디오 광고 데이터의 목록을 제공합니다.

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

## 광고 비디오 데이터 {#section_hq3_nbv_51b}

### 광고 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/>media.ad.id </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두  </li> <li> **샘플 값:**<br/> " 2125 " </li><li> **설명:**<br/>광고의 ID. (모든 정수 및/또는 문자 조합)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.na ME) </li> <li> **하트비트:**<br/> (s: 자산: ad_ id) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>방문 시 </li> <li> **보고서 이름:**<br/>광고 </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.na ME) </li> <li> **데이터 피드:**<br/>videoad </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.name) </li> </ul> |



### Pod의 광고 위치

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/>media.ad.podPosition </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>숫자 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 1 </li><li> **설명:**<br/>상위 광고 브레이크 내의 광고 위치 (색인) 입니다. 첫 번째 광고에는 색인 0, 두 번째 광고에 색인 1 등이 있습니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.po Dposition) </li> <li> **하트비트:**<br/> (s: 자산: pod_ position) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>Pod의 광고 위치의 </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.po Dposition) </li> <li> **데이터 피드:**<br/>videoadinpod </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### 광고 길이

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/>media.ad.length </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>숫자 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.1 </li> <li> **샘플 값:**<br/> " 15 "  </li><li> **설명:**<br/>비디오 광고 길이 (초)   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.le ngth) </li> <li> **하트비트:**<br/> (L: 자산: ad_ length) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar 및 분류 </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>광고 길이 및 광고 길이(변수) </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.le ngth) </li> <li> **데이터 피드:**<br/>videoadlength </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.length) </li> </ul> |



### 광고 플레이어 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/>media.ad.playerName </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> " Freewheel " </li><li> **설명:**<br/>광고 렌더링을 담당하는 플레이어의 이름입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.pl Ayername) </li> <li> **하트비트:**<br/> (s: SP: player_ name) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>광고 플레이어 이름 </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.pl Ayername) </li> <li> **데이터 피드:**<br/>videoadplayername </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### 광고 브레이크 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [이름](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/>media.ad.podFriendlyName </li> <li> **필수:**<br/> SDK: 예; API: 아니요. </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> " 프리롤 " </li><li> **설명:**<br/>광고의 친숙한 이름   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.po Dfriendlyname) </li> <li> **하트비트:**<br/> (s: 자산: pod_ name) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/>Pod 이름 </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.po Dfriendlyname) </li> <li> **데이터 피드:**<br/>videoadpod </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### 광고 브레이크 색인

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/>media.ad.podPosition </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>숫자 </li> <li> **전송 시점:**<br/> </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 1 </li><li> **설명:**<br/>컨텐츠 내에서 1 부터 시작하는 광고 분류의 인덱스입니다. 속성은 Media SDK에서 Pod ID를 생성하는 데&#x200B;**에만** 사용됩니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **하트비트:**<br/> </li> </ul> | <ul> <li> **사용 가능:**<br/>아니요 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/>N/A </li> <li> **컨텍스트 데이터:**<br/> </li> <li> **데이터 피드:**<br/> </li> <li> **Audience Manager:**<br/> </li> </ul> |



### 광고 브레이크 위치

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/>media.ad.podSecond </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>숫자 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 90 </li><li> **설명:**<br/>컨텐츠 내의 광고 나누기의 오프셋 (단위: 초)   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.po Dsecond) </li> <li> **하트비트:**<br/> (L: 자산: pod_ offset) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/>Pod 위치 </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.po Dsecond) </li> <li> **데이터 피드:**<br/> </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### 광고 브레이크 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> c 4 a 577424 c 84067899 b 807 c 76722 d 495_ 1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.po d) </li> <li> **하트비트:**<br/> (L: 자산: pod_ id) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>광고 Pod </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.po d) </li> <li> **데이터 피드:**<br/>videoadpod </li> <li> **Audience Manager:**<br/> </li> </ul> |



### 광고 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [이름](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/>media.ad.name </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.1 </li> <li> **샘플 값:**<br/> " Ford F -150 " </li><li> **설명:**<br/>광고의 친숙한 이름입니다. 보고 시 "광고 이름"은 분류이고, "광고 이름(변수)"은 eVar입니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.fr Iendlyname) </li> <li> **하트비트:**<br/> (s: 자산: ad_ name) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar 및 분류 </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>광고 이름 및 광고 이름(변수) </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.fr Iendlyname) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## 표준 광고 메타데이터 {#section_EFB805867916411E84DE1BA5A183D86A}

### 광고주

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>ADVERTISER </li> <li> **API 키:**<br/>media.ad.advertiser </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>광고에 제품이 포함된 회사/브랜드.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.ad Vertiser) </li> <li> **하트비트:**<br/> (s: META:<br/>a.media.ad.ad Vertiser) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> <i>광고주 </i> </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.ad Vertiser) </li> <li> **데이터 피드:**<br/>videoadvertiser </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### 캠페인 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>CAMPAIGN_ID </li> <li> **API 키:**<br/>media.ad.campaignId </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> 정수 또는 이름 (문자열) 입니다.  </li><li> **설명:**<br/>광고 캠페인의 ID.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.ca Mpaign) </li> <li> **하트비트:**<br/> (s: META:<br/>a.media.ad.ca 참조) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> <i>캠페인 ID </i> </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.ca Mpaign) </li> <li> **데이터 피드:**<br/>videocampaign </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.campaign) </li> </ul> |



### 광고 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>CREATIVE_ID </li> <li> **API 키:**<br/>media.ad.creativeId </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> 정수 또는 이름 (문자열) 입니다.  </li><li> **설명:**<br/>광고 크리에이티브 ID.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.cr Eative) </li> <li> **하트비트:**<br/> (s: META:<br/>a.media.ad.cr Eative) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> <i>광고 ID </i> </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.cr Eative) </li> <li> **데이터 피드:**<br/>adclassificationcreative </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.creative) </li> </ul> |



### 사이트 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>SITE_ID </li> <li> **API 키:**<br/>media.ad.siteId </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>광고 사이트의 ID.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.si TE) </li> <li> **하트비트:**<br/> (s: META:<br/>a.media.ad.si TE) </li> </ul> | <ul> <li> **사용 가능:**<br/> <i>사용자 지정 처리 규칙 사용 </i> </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> <i> </i> </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.si TE) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.site) </li> </ul> |



### 광고 URL

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>CREATIVE_URL </li> <li> **API 키:**<br/>media.ad.creativeURL </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>광고 크리에이티브 URL.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.cr Eativeurl) </li> <li> **하트비트:**<br/> (s: META:<br/>a.media.ad.cr Eativeurl) </li> </ul> | <ul> <li> **사용 가능:**<br/> <i>사용자 지정 처리 규칙 사용 </i> </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> <i> </i> </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.cr Eativeurl) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.creativeURL) </li> </ul> |



### 게재위치 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>PLACEMENT_ID </li> <li> **API 키:**<br/>media.ad.placementId </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>광고의 배치 ID.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.pl 획득) </li> <li> **하트비트:**<br/> (s: META:<br/>a.media.ad.pl Acement) </li> </ul> | <ul> <li> **사용 가능:**<br/> <i>사용자 지정 처리 규칙 사용 </i> </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> <i> </i> </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.pl 획득) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.placement) </li> </ul> |




## 광고 지표 {#section_22AA1565F11C4F3990E2AB51CD3213F7}

### 광고 시작

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> true </li><li> **설명:**<br/>비디오 광고 시작 수.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.vi EW) </li> <li> **하트비트:**<br/> (s: 이벤트: type = start)<br/> (s: 자산: type = ad) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>광고 시작 </li> <li> **데이터 피드:**<br/>videoadstart </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.vi EW) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.view) </li> </ul> |



### 광고 완료

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> true </li><li> **설명:**<br/>비디오 광고 수.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.com Plete) </li> <li> **하트비트:**<br/> (s: 이벤트: type = complete)<br/> (s: 자산: type = ad)  </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>광고 완료 </li> <li> **데이터 피드:**<br/>videoadcomplete </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.com Plete) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.complete) </li> </ul> |



### 광고 체류 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> **샘플 값:**<br/> 15 </li><li> **설명:**<br/>광고 시청 시간을 초 단위로 나타낸 총 시간 (초) 입니다. 값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다.  <br/>**릴리스 날짜: 2018년 9월 13일**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.ti Meplayed) </li> <li> **하트비트:**<br/> </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>광고 체류 시간 </li> <li> **데이터 피드:**<br/>videoadtime </li> <li> **컨텍스트 데이터:**<br/> (a.media.ad.ti Meplayed) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



## Related APIs {#section_Related_APIs}

### Createadobject API:

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### Createadbreakobject API:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### Mediaheartbeatconfig API:

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

