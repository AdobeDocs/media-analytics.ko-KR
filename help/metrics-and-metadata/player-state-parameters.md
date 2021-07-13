---
title: 플레이어 상태 매개 변수
description: '"전체 화면, 닫기 캡션, 음소거 및 사진 속성의 플레이어 상태 추적 매개 변수에 대해 알아봅니다."'
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: cd51ed3a-fe37-41e9-8243-dfd9deb514c1
feature: '"Media Analytics, 변수"'
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '2249'
ht-degree: 98%

---

# 플레이어 상태 매개 변수{#player-state-parameters}

이 항목에서는 솔루션 변수를 통해 Adobe가 수집하는 플레이어 상태 데이터의 목록을 제공합니다.

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

## 플레이어 상태 속성 {#player-state-properties}

플레이어 상태 추적 기능을 오디오 또는 비디오 스트림에 연결할 수 있습니다. 표준화된 플레이어 상태 추적 지표는 솔루션 변수로 저장됩니다. 표준 상태는 fullScreen, mute, closeCaption, pictureInPicture 및 inFocus입니다.

### 전체 화면 속성

#### 전체 화면 영향을 받는 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키**<br/> 자동으로 설정됨  </li> <li> **API 키**<br/> N/A </li> <li> **필수**<br/> 아니요 </li> <li> **유형**<br/> 숫자 </li> <li> **전송 시점**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전**<br/> 3.0</li> <li> **샘플 값**<br/> TRUE </li><li> **설명**<br/>&#x200B;전체 화면의 영향을 받은 스트림 수입니다. 이 지표는 재생 세션 중에 하나 이상의 전체 화면 상태가 발생한 경우에만 1로 설정됩니다. <br/> **중요**<br/> 이 이벤트가 설정된 경우 TRUE 값만 가능합니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.fullscreen.set<br/></li> <li> **Heartbeat**<br/> N/A </li> </ul> | <ul> <li> **사용 가능**<br/> 예 </li> <li> **예약된 변수**<br/> 이벤트 </li> <li> **보고서 이름**<br/> 전체 화면의 영향을 받은 스트림 </li> <li> **컨텍스트 데이터**<br/> a.media.states.fullscreen.set<br/> </li> <li> **데이터 피드**<br/> videostatefullscreen </li> <li> **Audience Manager**<br/> c_contextdata.a.media.states.fullscreen.set </li> </ul> |

#### 전체 화면 카운트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키**<br/> 자동으로 설정됨  </li> <li> **API 키**<br/> N/A </li> <li> **필수**<br/> 아니요 </li> <li> **유형**<br/> 숫자 </li> <li> **전송 시점**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전**<br/> 3.0</li> <li> **샘플 값**<br/> TRUE </li><li> **설명**<br/>&#x200B;전체 화면이 표시된 횟수입니다. 이 지표는 재생 세션 중에 하나 이상의 전체 화면 상태가 발생한 경우에만 1로 설정됩니다. <br/> **중요**<br/> 이 이벤트가 설정되면 개수는 비디오가 전체 화면 상태에 있었던 횟수와 같습니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.</li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.fullscreen.count<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> **사용 가능**<br/> 예 </li> <li> **예약된 변수**<br/> 이벤트 </li> <li> **보고서 이름**<br/> 전체 화면 수 </li> <li> **컨텍스트 데이터**<br/> a.media.states.fullscreen.count<br/> </li> <li> **데이터 피드**<br/> videostfullscreencount </li> <li> **Audience Manager**<br/> c_contextdata.media.states.fullscreen.count </li> </ul> |



#### 전체 화면 총 기간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키**<br/> 자동으로 설정됨  </li> <li> **API 키**<br/> N/A </li> <li> **필수**<br/> 아니요 </li> <li> **유형**<br/> 숫자 </li> <li> **전송 시점**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전**<br/> 3.0</li> <li> **샘플 값**<br/> TRUE </li><li> **설명**<br/>&#x200B;전체 화면이 표시된 시간 길이입니다. 이 지표는 재생 세션 중에 하나 이상의 전체 화면 상태가 발생한 경우에만 1로 설정됩니다. <br/> **중요**<br/>  이 이벤트가 설정되면 시간은 비디오가 전체 화면 상태에 있었던 시간과 같습니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.  </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.fullscreen.time<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> **사용 가능**<br/> 예 </li> <li> **예약된 변수**<br/> 이벤트 </li> <li> **보고서 이름**<br/> 전체 화면 총 시간 </li> <li> **컨텍스트 데이터**<br/> a.media.states.fullscreen.time<br/> </li> <li> **데이터 피드**<br/> videostfullscreen </li> <li> **Audience Manager**<br/> c_contextdata.media.states.fullscreen.time </li> </ul> |


### 닫힌 캡션 속성

#### 자막의 영향을 받는 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키**<br/> 자동으로 설정됨  </li> <li> **API 키**<br/> N/A </li> <li> **필수**<br/> 아니요 </li> <li> **유형**<br/> 숫자 </li> <li> **전송 시점**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전**<br/> 3.0</li> <li> **샘플 값**<br/> TRUE </li><li> **설명**<br/>&#x200B;닫힌 캡션의 영향을 받은 스트림 수입니다. 이 지표는 재생 세션 중에 하나 이상의 닫힌 캡션 상태가 발생한 경우에만 1로 설정됩니다. <br/> **중요**<br/> 이 이벤트가 설정된 경우 TRUE 값만 가능합니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.closedcaptioning.set<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> **사용 가능**<br/> 예 </li> <li> **예약된 변수**<br/> 이벤트 </li> <li> **보고서 이름**<br/> 닫힌 캡션의 영향을 받은 스트림 </li> <li> **컨텍스트 데이터**<br/> a.media.states.closedcaptioning.set<br/> </li> <li> **데이터 피드**<br/> videostlisedcaptioning </li> <li> **Audience Manager**<br/> c_contextdata.a.media.states.closedcaptioning.set </li> </ul> |


#### 자막 카운트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키**<br/> 자동으로 설정됨  </li> <li> **API 키**<br/> N/A </li> <li> **필수**<br/> 아니요 </li> <li> **유형**<br/> 숫자 </li> <li> **전송 시점**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전**<br/> 3.0</li> <li> **샘플 값**<br/> TRUE </li><li> **설명**<br/>&#x200B;자막이 표시된 횟수입니다. 이 지표는 재생 세션 중에 하나 이상의 닫힌 캡션 상태가 발생한 경우에만 1로 설정됩니다. <br/> **중요**<br/>  이 이벤트가 설정되면 개수는 비디오가 자막 상태에 있었던 횟수와 같습니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.states.closedcaptioning.count<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> **사용 가능**<br/> 예 </li> <li> **예약된 변수**<br/> 이벤트 </li> <li> **보고서 이름**<br/> 자막 수 </li> <li> **컨텍스트 데이터**<br/> a.media.states.closedcaptioning.count<br/> </li> <li> **데이터 피드**<br/> videostlosedcaptioncount </li> <li> **Audience Manager**<br/> c_contextdata.media.states.closedcaptioning.count </li> </ul> |


#### 자막 총 기간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키**<br/> 자동으로 설정됨  </li> <li> **API 키**<br/> N/A </li> <li> **필수**<br/> 아니요 </li> <li> **유형**<br/> 숫자 </li> <li> **전송 시점**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전**<br/> 3.0</li> <li> **샘플 값**<br/> TRUE </li><li> **설명**<br/>&#x200B;자막이 표시된 시간입니다. 이 지표는 재생 세션 중에 하나 이상의 전체 화면 상태가 발생한 경우에만 1로 설정됩니다. <br/> **중요**<br/>  이 이벤트가 설정되면 시간은 비디오가 자막 상태에서 있었던 시간과 같습니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.closedcaptioning.time<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> **사용 가능**<br/> 예 </li> <li> **예약된 변수**<br/> 이벤트 </li> <li> **보고서 이름**<br/> 자막 총 시간 </li> <li> **컨텍스트 데이터**<br/> a.media.states.closedcaptioning.time<br/> </li> <li> **데이터 피드**<br/> videostateclosedcaptioningtime </li> <li> **Audience Manager**<br/> c_contextdata.media.states.closedcaptioning.time </li> </ul> |


### 음소거 속성

#### 음소거의 영향을 받는 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키**<br/> 자동으로 설정됨  </li> <li> **API 키**<br/> N/A </li> <li> **필수**<br/> 아니요 </li> <li> **유형**<br/> 숫자 </li> <li> **전송 시점**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전**<br/> 3.0</li> <li> **샘플 값**<br/> TRUE </li><li> **설명**<br/>&#x200B;음소거의 영향을 받은 스트림 수입니다. 이 지표는 재생 세션 중에 하나 이상의 음소거 상태가 발생한 경우에만 1로 설정됩니다. <br/> **중요**<br/> 이 이벤트가 설정된 경우 TRUE 값만 가능합니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.mute.set<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> **사용 가능**<br/> 예 </li> <li> **예약된 변수**<br/> 이벤트 </li> <li> **보고서 이름**<br/> 음소거의 영향을 받은 스트림 </li> <li> **컨텍스트 데이터**<br/> a.media.states.mute.set<br/> </li> <li> **데이터 피드**<br/> videostatemute </li> <li> **Audience Manager**<br/> c_contextdata.a.media.states.mute.set </li> </ul> |

#### 음소거 카운트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키**<br/> 자동으로 설정됨  </li> <li> **API 키**<br/> N/A </li> <li> **필수**<br/> 아니요 </li> <li> **유형**<br/> 숫자 </li> <li> **전송 시점**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전**<br/> 3.0</li> <li> **샘플 값**<br/> TRUE </li><li> **설명**<br/> 음소거가 표시된 횟수입니다. 이 지표는 재생 세션 중에 하나 이상의 음소거 상태가 발생한 경우에만 1로 설정됩니다. <br/> **중요**<br/>  이 이벤트가 설정되면 개수는 비디오가 음소거 상태에 있었던 횟수와 같습니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.mute.count<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> **사용 가능**<br/> 예 </li> <li> **예약된 변수**<br/> 이벤트 </li> <li> **보고서 이름**<br/> 음소거 수 </li> <li> **컨텍스트 데이터**<br/> a.media.states.mute.count<br/> </li> <li> **데이터 피드**<br/> videostatemutecount </li> <li> **Audience Manager**<br/> c_contextdata.media.states.mute.count </li> </ul> |

#### 음소거 총 기간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키**<br/> 자동으로 설정됨  </li> <li> **API 키**<br/> N/A </li> <li> **필수**<br/> 아니요 </li> <li> **유형**<br/> 숫자 </li> <li> **전송 시점**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전**<br/> 3.0</li> <li> **샘플 값**<br/> TRUE </li><li> **설명**<br/> 음소거가 표시된 시간입니다. 이 지표는 재생 세션 중에 하나 이상의 음소거 상태가 발생한 경우에만 1로 설정됩니다. <br/> **중요**<br/> 이 이벤트가 설정되면 시간은 비디오가 음소거 상태에서 있었던 시간과 같습니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.mute.time<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> **사용 가능**<br/> 예 </li> <li> **예약된 변수**<br/> 이벤트 </li> <li> **보고서 이름**<br/> 음소거 총 시간 </li> <li> **컨텍스트 데이터**<br/> a.media.states.mute.time<br/> </li> <li> **데이터 피드**<br/> videostatemutetime </li> <li> **Audience Manager**<br/> c_contextdata.media.states.mute.time </li> </ul> |


### 화면 속 화면 속성


#### 화면 속 화면의 영향을 받은 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키**<br/> 자동으로 설정됨  </li> <li> **API 키**<br/> N/A </li> <li> **필수**<br/> 아니요 </li> <li> **유형**<br/> 숫자 </li> <li> **전송 시점**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전**<br/> 3.0</li> <li> **샘플 값**<br/> TRUE </li><li> **설명**<br/>&#x200B;화면 속 화면의 영향을 받은 스트림의 수입니다. 이 지표는 재생 세션 중에 화면 속 화면 상태가 발생한 경우에만 1로 설정됩니다. <br/> **중요**<br/> 이 이벤트가 설정된 경우 TRUE 값만 가능합니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.pictureinpicture.set<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> **사용 가능**<br/> 예 </li> <li> **예약된 변수**<br/> 이벤트 </li> <li> **보고서 이름**<br/> 화면 속 화면의 영향을 받은 스트림 </li> <li> **컨텍스트 데이터**<br/> a.media.states.pictureinpicture.set<br/> </li> <li> **데이터 피드**<br/> videostacepictureinpicture </li> <li> **Audience Manager**<br/> c_contextdata.a.media.states.pictureinpicture.set </li> </ul> |


#### 화면 속 화면 카운트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키**<br/> 자동으로 설정됨  </li> <li> **API 키**<br/> N/A </li> <li> **필수**<br/> 아니요 </li> <li> **유형**<br/> 숫자 </li> <li> **전송 시점**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전**<br/> 3.0</li> <li> **샘플 값**<br/> TRUE </li><li> **설명**<br/>&#x200B;화면 속 화면을 표시한 횟수입니다. 이 지표는 재생 세션 중에 화면 속 화면 상태가 발생한 경우에만 1로 설정됩니다. <br/> **중요** <br/> 이 이벤트가 설정되면 개수는 화면 속 화면 상태에 있었던 횟수와 같습니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.pictureinpicture.count<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> **사용 가능**<br/> 예 </li> <li> **예약된 변수**<br/> 이벤트 </li> <li> **보고서 이름**<br/> 화면 속 화면 수 </li> <li> **컨텍스트 데이터**<br/> a.media.states.pictureinpicture.count<br/> </li> <li> **데이터 피드**<br/> videostacepicturepresentation </li> <li> **Audience Manager**<br/> c_contextdata.media.states.pictureinpicture.count </li> </ul> |


#### 화면 속 화면 총 기간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키**<br/> 자동으로 설정됨  </li> <li> **API 키**<br/> N/A </li> <li> **필수**<br/> 아니요 </li> <li> **유형**<br/> 숫자 </li> <li> **전송 시점**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전**<br/> 3.0</li> <li> **샘플 값**<br/> TRUE </li><li> **설명**<br/>&#x200B;화면 속 화면을 표시한 시간 길이입니다. 이 지표는 재생 세션 중에 화면 속 화면 상태가 발생한 경우에만 1로 설정됩니다. <br/> **중요** <br/> 이 이벤트가 설정되면 시간은 비디오가 화면 속 화면 상태에 있었던 시간과 같습니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다..   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.pictureinpicture.time<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> **사용 가능**<br/> 예 </li> <li> **예약된 변수**<br/> 이벤트 </li> <li> **보고서 이름**<br/> 화면 속 화면 총 시간 </li> <li> **컨텍스트 데이터**<br/> a.media.states.pictureinpicture.time<br/> </li> <li> **데이터 피드**<br/> videostacepicturetime </li> <li> **Audience Manager**<br/> c_contextdata.media.states.pictureinpicture.time </li> </ul> |


### 초점 속성

#### 초점의 영향을 받는 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키**<br/> 자동으로 설정됨  </li> <li> **API 키**<br/> N/A </li> <li> **필수**<br/> 아니요 </li> <li> **유형**<br/> 숫자 </li> <li> **전송 시점**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전**<br/> 3.0</li> <li> **샘플 값**<br/> TRUE </li><li> **설명**<br/>&#x200B;초점의 영향을 받은 스트림 수입니다. 이 지표는 재생 세션 중에 초점 상태가 발생한 경우에만 1로 설정됩니다. <br/> **중요**<br/> 이 이벤트가 설정된 경우 TRUE 값만 가능합니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.infocus.set<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> **사용 가능**<br/> 예 </li> <li> **예약된 변수**<br/> 이벤트 </li> <li> **보고서 이름**<br/> 초점의 영향을 받은 스트림 </li> <li> **컨텍스트 데이터**<br/> a.media.states.infocus.set<br/> </li> <li> **데이터 피드**<br/> videostateinfocus </li> <li> **Audience Manager**<br/> c_contextdata.a.media.states.infocus.set </li> </ul> |


#### 초점 카운트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키**<br/> 자동으로 설정됨  </li> <li> **API 키**<br/> N/A </li> <li> **필수**<br/> 아니요 </li> <li> **유형**<br/> 숫자 </li> <li> **전송 시점**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전**<br/> 3.0</li> <li> **샘플 값**<br/> TRUE </li><li> **설명**<br/>&#x200B;초점을 표시한 횟수입니다. 이 지표는 재생 세션 중에 초점 상태가 발생한 경우에만 1로 설정됩니다. <br/> **중요**<br/>  이 이벤트가 설정되면 개수는 비디오가 초점 상태에 있었던 횟수와 같습니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.infocus.count<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> **사용 가능**<br/> 예 </li> <li> **예약된 변수**<br/> 이벤트 </li> <li> **보고서 이름**<br/> 초점 수 </li> <li> **컨텍스트 데이터**<br/> a.media.states.infocus.count<br/> </li> <li> **데이터 피드**<br/> videostateinfocuscount </li> <li> **Audience Manager**<br/> c_contextdata.media.states.infocus.count </li> </ul> |


#### 초점 총 기간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키**<br/> 자동으로 설정됨  </li> <li> **API 키**<br/> N/A </li> <li> **필수**<br/> 아니요 </li> <li> **유형**<br/> 숫자 </li> <li> **전송 시점**<br/> 미디어 닫기 </li> <li> **최소. SDK 버전**<br/> 3.0</li> <li> **샘플 값**<br/> TRUE </li><li> **설명**<br/>&#x200B;초점을 표시한 시간 길이입니다. 이 지표는 재생 세션 중에 초점 상태가 발생한 경우에만 1로 설정됩니다. <br/> **중요** <br/> 이 이벤트가 설정되면 시간은 비디오가 초점 상태에서 있었던 시간과 같습니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.infocus.time<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> **사용 가능**<br/> 예 </li> <li> **예약된 변수**<br/> 이벤트 </li> <li> **보고서 이름**<br/> 초점 총 시간 </li> <li> **컨텍스트 데이터**<br/> a.media.states.infocus.time<br/> </li> <li> **데이터 피드**<br/> videostateinfocustime </li> <li> **Audience Manager**<br/> c_contextdata.media.states.infocus.time </li> </ul> |

## XDM ID에 대한 속성 목록

Analytics에 저장된 데이터는 어떤 목적으로든 사용할 수 있으며, 플레이어 상태 지표는 XDM을 사용하여 Adobe Experience Platform으로 가져와서 Customer Journey Analytics와 함께 사용할 수 있습니다.

| 플레이어 상태 속성 | 매핑 |
|---------------------------------------|------------------------------------|
| a.media.states.fullScreen.set | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateSet |
| a.media.states.fullScreen.count | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateCount |
| a.media.states.fullScreen.time | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateTime |
| a.media.states.mute.set | media.mediaTimed.primaryAssetViewDetails.mute.playerStateSet |
| a.media.states.mute.count | media.mediaTimed.primaryAssetViewDetails.mute.playerStateCount |
| a.media.states.mute.time | media.mediaTimed.primaryAssetViewDetails.mute.playerStateTime |
| a.media.states.closeCaption.set | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateSet |
| a.media.states.closeCaption.count | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateCount |
| a.media.states.closeCaption.time | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateTime |
| a.media.states.pictureInPicture.set | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateSet |
| a.media.states.pictureInPicture.count | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateCount |
| a.media.states.pictureInPicture.time | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateTime |
| a.media.states.inFocus.set | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateSet |
| a.media.states.inFocus.count | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateCount |
| a.media.states.inFocus.time | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateTime |

## 관련 API {#related_apis_section}

* Android - [createStateObject](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* iOS - [createStateObjectWithName](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* Javascript - [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)
