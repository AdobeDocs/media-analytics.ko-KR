---
seo-title: 광고 매개 변수
title: 광고 매개 변수
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
translation-type: tm+mt
source-git-commit: 4a14e2faae6401a3f885eb5e341c1344d7f1e94d

---


# 광고 매개 변수{#ad-parameters}

이 항목에서는 컨텍스트 데이터 값을 포함하여 Adobe에서 솔루션 변수를 통해 수집하는 비디오 광고 데이터의 목록을 제공합니다.

테이블 데이터 설명:

* **구현:**&#x200B;구현 값 및 요구 사항에 대한 정보
   * *키* - 앱에서 수동으로 설정하거나 Adobe Media SDK에 의해 자동으로 설정된 변수.
   * *필수* - 기본 비디오 추적에 매개 변수가 필요한지 여부를 나타냅니다.
   * *유형* - 설정할 변수의 유형(문자열 또는 숫자)을 지정합니다.
   * *Sent With - Indicates when the data is sent: Media Start is the analytics call sent on media start, Ad Start is the analytics call sent on ad start, and so on; the Close calls are the compiled analytics calls sent directly from the heartbeat server to the analytics server at the end of the media session, or the end of the ad, chapter, etc.******* 닫기 호출은 네트워크 패킷 호출에서 사용할 수 없습니다.
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
>아래 나열된 변수에 대한 분류 이름을 변경하지 마십시오.
>보고/예약 변수에 "분류"로 설명되어 있습니다.
>미디어 분류는 보고서 세트가 미디어에 대해 활성화될 때 정의됩니다
>tracking. Adobe는 수시로 새로운 속성을 추가하고 이러한 상황이 발생하면
>고객은 보고서 세트를 다시 활성화하여 새 미디어에 액세스해야 합니다.
>속성을 참조하십시오. 업데이트 프로세스 동안 Adobe는
>분류는 변수의 이름을 확인하여 활성화됩니다. If any of
>누락된 경우 Adobe에서 누락된 항목을 다시 추가합니다.

## 광고 비디오 데이터 {#section_hq3_nbv_51b}

### 광고 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/>media.ad.id </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두  </li> <li> ****<br/> 샘플 값:"2125" </li><li> **설명:**<br/>광고의 ID입니다. (모든 정수 및/또는 문자 조합)  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>이름) </li> <li> **Heartbeat:**<br/> (s:asset:ad_id) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>방문 시 </li> <li> **보고서 이름:**<br/>광고 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.ad.<br/>이름) </li> <li> **데이터 피드:**<br/>videoad </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.name) </li> </ul> |



### Pod의 광고 위치

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/>media.ad.podPosition </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>숫자 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:1 </li><li> **설명:**<br/>상위 광고 브레이크 내의 광고의 위치(인덱스)입니다. 첫 번째 광고에는 색인 0, 두 번째 광고에 색인 1 등이 있습니다.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>podPosition) </li> <li> ****<br/> Heartbeat: (s:asset:pod_position) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>Pod의 광고 위치의 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.ad.<br/>podPosition) </li> <li> **데이터 피드:**<br/>videoadinpod </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### 광고 길이

|   구현   | Network Parameters | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/>media.ad.length </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>숫자 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.1 </li> <li> **Sample Value:**<br/> "15"  </li><li> **Description:**<br/>Length of video ad in seconds.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>length) </li> <li> ****<br/> 하트비트:(l:asset:ad_length) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar 및 분류 </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>광고 길이 및 광고 길이(변수) </li> <li> ****<br/> 컨텍스트 데이터:(a.media.ad.<br/>length) </li> <li> **데이터 피드:**<br/>videoadlength </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.length) </li> </ul> |



### 광고 플레이어 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/>media.ad.playerName </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:"자유로운 바퀴" </li><li> **Description:**<br/>The name of the player responsible for rendering the ad.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>playerName) </li> <li> **Heartbeat:**<br/> (s:sp:player_name) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>광고 플레이어 이름 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.ad.<br/>playerName) </li> <li> **데이터 피드:**<br/>videoadplayername </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### 광고 브레이크 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [이름](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/>media.ad.podFriendlyName </li> <li> ****<br/> 필수:SDK:예;API:아니 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:"프리롤" </li><li> **설명:**<br/>광고 분리의 친숙한 이름입니다.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>podFriendlyName) </li> <li> **Heartbeat:**<br/> (s:asset:pod_name) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/>Pod 이름 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.ad.<br/>podFriendlyName) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### 광고 브레이크 색인

|   구현   | Network Parameters | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/>media.ad.podPosition </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>숫자 </li> <li> **전송 시점:**<br/> </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> Sample Value: 1 </li><li> **Description:The index of the ad break inside the content starting at 1.**<br/> 속성은 Media SDK에서 Pod ID를 생성하는 데&#x200B;**에만** 사용됩니다.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **하트비트:**<br/> </li> </ul> | <ul> <li> **사용 가능:**<br/>아니요 </li> <li> **예약된 변수:**<br/>N/A </li> <li> **보고서 이름:**<br/>N/A </li> <li> **컨텍스트 데이터:**<br/> </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> </li> </ul> |



### 광고 브레이크 위치

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/>media.ad.podSecond </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/>숫자 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:90년 </li><li> **설명:**<br/>컨텐츠 내에서 광고 분리의 오프셋(초)입니다.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>podSecond) </li> <li> ****<br/> 하트비트:(l:asset:pod_offset) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>분류 </li> <li> **보고서 이름:**<br/>Pod 위치 </li> <li> ****<br/> 컨텍스트 데이터:(a.media.ad.<br/>podSecond) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### 광고 브레이크 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>창) </li> <li> **Heartbeat:**<br/> (s:asset:pod_id) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>광고 Pod </li> <li> ****<br/> Context Data: (a.media.ad.<br/>창) </li> <li> **데이터 피드:**<br/>videoadpod </li> <li> **Audience Manager:**<br/> </li> </ul> |



### 광고 이름

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>  [이름](./ad-parameters.md#section_Related_APIs) </li> <li> **API 키:**<br/>media.ad.name </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.1 </li> <li> ****<br/> 샘플 값:"Ford F-150" </li><li> **설명:**<br/>광고의 친숙한 이름입니다.  보고 시 "광고 이름"은 분류이고, "광고 이름(변수)"은 eVar입니다.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>friendlyName) </li> <li> ****<br/> 하트비트:(s:asset:ad_name) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar 및 분류 </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/>광고 이름 및 광고 이름(변수) </li> <li> ****<br/> Context Data: (a.media.ad.<br/>friendlyName) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## 표준 광고 메타데이터 {#section_EFB805867916411E84DE1BA5A183D86A}

### 광고주

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>ADVERTISER </li> <li> **API 키:**<br/>media.ad.advertiser </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **Sample Value:**<br/> </li><li> **Description:Company/Brand whose product is featured in the ad.**<br/>   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>advertiser) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> <i>광고주 </i> </li> <li> ****<br/> 컨텍스트 데이터:(a.media.ad.<br/>advertiser) </li> <li> **데이터 피드:**<br/>videoadvertiser </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### 캠페인 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>CAMPAIGN_ID </li> <li> **API 키:**<br/>media.ad.campaignId </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> ****<br/> 샘플 값:정수 또는 이름(문자열)입니다.  </li><li> **설명:**<br/>광고 캠페인의 ID입니다.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>campaign) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.ad.cacampaign) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> <i>캠페인 ID </i> </li> <li> ****<br/> 컨텍스트 데이터:(a.media.ad.<br/>campaign) </li> <li> **데이터 피드:**<br/>videocampaign </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.campaign) </li> </ul> |



### 광고 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>CREATIVE_ID </li> <li> **API 키:**<br/>media.ad.creativeId </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> ****<br/> 샘플 값:정수 또는 이름(문자열)입니다.  </li><li> **설명:**<br/>광고 크리에이티브의 ID입니다.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>creative) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.ad.creative) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> <i>광고 ID </i> </li> <li> ****<br/> 컨텍스트 데이터:(a.media.ad.<br/>creative) </li> <li> **데이터 피드:**<br/>adclassificationcreative </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.creative) </li> </ul> |



### 사이트 ID

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>SITE_ID </li> <li> **API 키:**<br/>media.ad.siteId </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>광고 사이트의 ID.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>없습니다) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.ad.site) </li> </ul> | <ul> <li> **사용 가능:**<br/> <i>Use custom processing rule </i> </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> <i> </i> </li> <li> ****<br/> 컨텍스트 데이터:(a.media.ad.<br/>없습니다) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.site) </li> </ul> |



### 광고 URL

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>CREATIVE_URL </li> <li> **API 키:**<br/>media.ad.creativeURL </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **샘플 값:**<br/> </li><li> **설명:**<br/>광고 크리에이티브의 URL.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>creativeURL) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **사용 가능:**<br/> <i>사용자 지정 처리 규칙 사용 </i> </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> <i> </i> </li> <li> ****<br/> 컨텍스트 데이터:(a.media.ad.<br/>creativeURL) </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.creativeURL) </li> </ul> |



### 게재위치 ID

|   구현   | Network Parameters | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>PLACEMENT_ID </li> <li> **API 키:**<br/>media.ad.placementId </li> <li> **필수:**<br/>아니요 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작, 광고 종료 </li> <li> **최소. SDK 버전:** 1.5.7 </li> <li> **Sample Value:**<br/> </li><li> **Description:**<br/>Placement ID of the ad.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>배치) </li> <li> ****<br/> 하트비트:(s:meta:<br/>a.media.ad.placement) </li> </ul> | <ul> <li> **사용 가능:**<br/> <i>사용자 지정 처리 규칙 사용 </i> </li> <li> **예약된 변수:**<br/>eVar </li> <li> **만료:**<br/>히트 시 </li> <li> **보고서 이름:**<br/> <i> </i> </li> <li> ****<br/> 컨텍스트 데이터:(a.media.ad.<br/>배치) </li> <li> **데이터 피드:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.placement) </li> </ul> |




## 광고 지표 {#section_22AA1565F11C4F3990E2AB51CD3213F7}

### 광고 시작

|   구현   | Network Parameters | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 시작 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:TRUE </li><li> **Description:**<br/>Number of video ad starts.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>view) </li> <li> ****<br/> 하트비트: (s:event:type=start)<br/> (s:asset:type=ad) </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>광고 시작 </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> 컨텍스트 데이터:(a.media.ad.<br/>view) </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.view) </li> </ul> |



### 광고 완료

|   구현   | Network Parameters | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:TRUE </li><li> **설명:**<br/>비디오 광고 완료 횟수입니다.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>완료됨) </li> <li> ****<br/> 하트비트:(s:event:type=complete)<br/> (s:asset:type=ad)  </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>광고 완료 </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> 컨텍스트 데이터:(a.media.ad.<br/>완료됨) </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.complete) </li> </ul> |



### 광고 체류 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키:**<br/>자동으로 설정됨 </li> <li> **API 키:**<br/>N/A </li> <li> **필수:**<br/>예 </li> <li> **유형:**<br/> 문자열 </li> <li> **전송 시점:**<br/>광고 닫기 </li> <li> **최소. SDK 버전:**&#x200B;모두 </li> <li> ****<br/> 샘플 값:15년 </li><li> **설명:**<br/>광고를 시청하는 데 걸린 총 시간(초)입니다(즉, 재생된 시간).  값은 Analysis Workspace 및 Reports &amp; Analytics에서 시간 형식(HH:MM:SS)으로 표시됩니다. 데이터 피드, Data Warehouse 및 보고 API에서는 값이 초 단위로 표시됩니다.  <br/>**릴리스 날짜: 2018년 9월 13일**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>timePlayed) </li> <li> **하트비트:**<br/> </li> </ul> | <ul> <li> **사용 가능:**<br/>예 </li> <li> **예약된 변수:**<br/>이벤트 </li> <li> **보고서 이름:**<br/>광고 체류 시간 </li> <li> **데이터 피드:**<br/>N/A </li> <li> ****<br/> Context Data: (a.media.ad.<br/>timePlayed) </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



## Related APIs {#section_Related_APIs}

### createAdObject API:

* Android - createAdObject[](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### createAdBreakObject API:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### MediaHeartbeatConfig API:

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

