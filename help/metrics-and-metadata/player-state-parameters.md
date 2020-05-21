---
title: 플레이어 상태 매개 변수
description: 이 항목에서는 플레이어 상태 추적 매개 변수에 대해 설명합니다.
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 3c24b69265287084393be830193da14ae85cc5ba
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 28%

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

플레이어 상태 추적 속성 테이블은 다음 5개 섹션으로 구성됩니다.

* 전체 화면
   * 전체 화면으로 영향을 받는 스트림
   * 전체 화면 수
   * 전체 화면 총 지속 시간
* 캡션 닫기
   * 자막 영향을 받는 스트림
   * 자막 수
   * 자막 총 지속 시간
* 음소거
   * 음소거 영향을 받은 스트림
   * 음소거 카운트
   * 총 음소거 기간
* 사진 속 사진
   * 그림의 영향을 받는 스트림
   * 사진 수
   * 그림 합계 기간
* 초점
   * 초점이 영향을 받는 스트림
   * 초점 카운트
   * 초점 총 기간

### 전체 화면 속성

#### 전체 화면으로 영향을 받는 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키&#x200B;**<br/>자동 설정</li> <li> **API 키&#x200B;**<br/>해당 사항 없음</li> <li> **필수&#x200B;**<br/>아니오</li> <li> **문자&#x200B;**<br/>번호</li> <li> **미디어 닫기로&#x200B;**<br/>전송</li> <li> **최소. SDK Version **<br/>3.0</li> <li> **샘플 값&#x200B;**<br/>TRUE</li><li> **설명&#x200B;**<br/>전체 화면으로 인해 영향을 받는 스트림 수입니다. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **중요** 이 이벤트가 설정되면 가능한 값만 TRUE입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.fullscreen.set)<br/></li> <li> **하트비트&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **사용 가능&#x200B;**<br/>예</li> <li> **예약된 변수&#x200B;**<br/>이벤트</li> <li> **보고서 이름&#x200B;**<br/>전체 화면으로 인해 영향을 받는 스트림</li> <li> **컨텍스트 데이터&#x200B;**<br/>(a.media.states.fullscreen.set)<br/> </li> <li> **데이터 피드&#x200B;**<br/>videostatefullscreen</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.fullscreen.set)</li> </ul> |

#### 전체 화면 수

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키&#x200B;**<br/>자동 설정</li> <li> **API 키&#x200B;**<br/>해당 사항 없음</li> <li> **필수&#x200B;**<br/>아니오</li> <li> **문자&#x200B;**<br/>번호</li> <li> **미디어 닫기로&#x200B;**<br/>전송</li> <li> **최소. SDK Version **<br/>3.0</li> <li> **샘플 값&#x200B;**<br/>TRUE</li><li> **설명&#x200B;**<br/>전체 화면이 표시된 횟수입니다. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **중요** 이 이벤트가 설정되면 가능한 값만 TRUE입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostumfullscreencount)<br/></li> <li> **하트비트&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **사용 가능&#x200B;**<br/>예</li> <li> **예약된 변수&#x200B;**<br/>이벤트</li> <li> **보고서 이름&#x200B;**<br/>전체 화면 수</li> <li> **컨텍스트 데이터&#x200B;**<br/>(videostumfullscreencount)<br/> </li> <li> **데이터 피드&#x200B;**<br/>videostfullscreencount</li> <li> **Audience Manager **<br/>(c_contextdata.videstatefullscreencount)</li> </ul> |



#### 전체 화면 총 지속 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키&#x200B;**<br/>자동 설정</li> <li> **API 키&#x200B;**<br/>해당 사항 없음</li> <li> **필수&#x200B;**<br/>아니오</li> <li> **문자&#x200B;**<br/>번호</li> <li> **미디어 닫기로&#x200B;**<br/>전송</li> <li> **최소. SDK Version **<br/>3.0</li> <li> **샘플 값&#x200B;**<br/>TRUE</li><li> **설명&#x200B;**<br/>전체 화면이 표시되는 시간입니다. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **중요** 이 이벤트가 설정되면 가능한 값만 TRUE입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostumfullscreen)<br/></li> <li> **하트비트&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **사용 가능&#x200B;**<br/>예</li> <li> **예약된 변수&#x200B;**<br/>이벤트</li> <li> **보고서 이름&#x200B;**<br/>전체 화면 기간</li> <li> **컨텍스트 데이터&#x200B;**<br/>(videostfullscreen)<br/> </li> <li> **데이터 피드&#x200B;**<br/>videostfullscreen</li> <li> **Audience Manager **<br/>(c_contextdata.videostfullscreen)</li> </ul> |


### 캡션 속성 닫기

#### 자막 영향을 받는 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키&#x200B;**<br/>자동 설정</li> <li> **API 키&#x200B;**<br/>해당 사항 없음</li> <li> **필수&#x200B;**<br/>아니오</li> <li> **문자&#x200B;**<br/>번호</li> <li> **미디어 닫기로&#x200B;**<br/>전송</li> <li> **최소. SDK Version **<br/>3.0</li> <li> **샘플 값&#x200B;**<br/>TRUE</li><li> **설명&#x200B;**<br/>자막 영향을 받는 스트림의 수입니다. This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **중요** 이 이벤트가 설정되면 가능한 값만 TRUE입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.closedcaptioning.set)<br/></li> <li> **하트비트&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **사용 가능&#x200B;**<br/>예</li> <li> **예약된 변수&#x200B;**<br/>이벤트</li> <li> **자막에&#x200B;**<br/>의해 영향을 받는 보고서 이름 스트림</li> <li> **컨텍스트 데이터&#x200B;**<br/>(a.media.states.closedcaptioning.set)<br/> </li> <li> **데이터 피드&#x200B;**<br/>videostlisedcaptioning</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.closedcaptioning.set)</li> </ul> |


#### 자막 수

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키&#x200B;**<br/>자동 설정</li> <li> **API 키&#x200B;**<br/>해당 사항 없음</li> <li> **필수&#x200B;**<br/>아니오</li> <li> **문자&#x200B;**<br/>번호</li> <li> **미디어 닫기로&#x200B;**<br/>전송</li> <li> **최소. SDK Version **<br/>3.0</li> <li> **샘플 값&#x200B;**<br/>TRUE</li><li> **설명&#x200B;**<br/>자막을 선택한 횟수입니다. This metric is set to 1 only if at least one Closed Captioning State occurred during a playback session.<br/> **중요** 이 이벤트가 설정되면 가능한 값만 TRUE입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatelosedcaptioningcount)<br/></li> <li> **하트비트&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **사용 가능&#x200B;**<br/>예</li> <li> **예약된 변수&#x200B;**<br/>이벤트</li> <li> **보고서 이름&#x200B;**<br/>자막 수</li> <li> **컨텍스트 데이터&#x200B;**<br/>(videstatelosedcaptioncount)<br/> </li> <li> **데이터 피드&#x200B;**<br/>videostlosedcaptioncount</li> <li> **Audience Manager **<br/>(c_contextdata.videstatelosedcaptioningcount)</li> </ul> |


#### 자막 총 지속 시간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키&#x200B;**<br/>자동 설정</li> <li> **API 키&#x200B;**<br/>해당 사항 없음</li> <li> **필수&#x200B;**<br/>아니오</li> <li> **문자&#x200B;**<br/>번호</li> <li> **미디어 닫기로&#x200B;**<br/>전송</li> <li> **최소. SDK Version **<br/>3.0</li> <li> **샘플 값&#x200B;**<br/>TRUE</li><li> **설명&#x200B;**<br/>자막 기간이 선택되었습니다. This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **중요** 이 이벤트가 설정되면 가능한 값만 TRUE입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatelosedcaptioningtime)<br/></li> <li> **하트비트&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **사용 가능&#x200B;**<br/>예</li> <li> **예약된 변수&#x200B;**<br/>이벤트</li> <li> **보고서 이름&#x200B;**<br/>자막 기간</li> <li> **컨텍스트 데이터&#x200B;**<br/>(videstatelosedcaptiontime)<br/> </li> <li> **데이터 피드&#x200B;**<br/>비디오시작캡션</li> <li> **Audience Manager **<br/>(c_contextdata.videstatelosedcaptioningtime)</li> </ul> |


### 속성 음소거

#### 음소거 영향을 받은 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키&#x200B;**<br/>자동 설정</li> <li> **API 키&#x200B;**<br/>해당 사항 없음</li> <li> **필수&#x200B;**<br/>아니오</li> <li> **문자&#x200B;**<br/>번호</li> <li> **미디어 닫기로&#x200B;**<br/>전송</li> <li> **최소. SDK Version **<br/>3.0</li> <li> **샘플 값&#x200B;**<br/>TRUE</li><li> **설명&#x200B;**<br/>음소거 영향을 받는 스트림 수입니다. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **중요** 이 이벤트가 설정되면 가능한 값만 TRUE입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.mute.set)<br/></li> <li> **하트비트&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **사용 가능&#x200B;**<br/>예</li> <li> **예약된 변수&#x200B;**<br/>이벤트</li> <li> **보고서 이름&#x200B;**<br/>음소거 영향을 받은 스트림</li> <li> **컨텍스트 데이터&#x200B;**<br/>(a.media.states.mute.set)<br/> </li> <li> **데이터 피드&#x200B;**<br/>비디오 구문</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.mute.set)</li> </ul> |

#### 음소거 카운트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키&#x200B;**<br/>자동 설정</li> <li> **API 키&#x200B;**<br/>해당 사항 없음</li> <li> **필수&#x200B;**<br/>아니오</li> <li> **문자&#x200B;**<br/>번호</li> <li> **미디어 닫기로&#x200B;**<br/>전송</li> <li> **최소. SDK Version **<br/>3.0</li> <li> **샘플 값&#x200B;**<br/>TRUE</li><li> **설명&#x200B;**<br/>음소거를 선택한 횟수입니다. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **중요** 이 이벤트가 설정되면 가능한 값만 TRUE입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatemutcount)<br/></li> <li> **하트비트&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **사용 가능&#x200B;**<br/>예</li> <li> **예약된 변수&#x200B;**<br/>이벤트</li> <li> **보고서 이름&#x200B;**<br/>음소거 수</li> <li> **컨텍스트 데이터&#x200B;**<br/>(videostatemutcount)<br/> </li> <li> **데이터 피드&#x200B;**<br/>비디오 상태</li> <li> **Audience Manager **<br/>(c_contextdata.videostatemutcount)</li> </ul> |

#### 총 음소거 기간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키&#x200B;**<br/>자동 설정</li> <li> **API 키&#x200B;**<br/>해당 사항 없음</li> <li> **필수&#x200B;**<br/>아니오</li> <li> **문자&#x200B;**<br/>번호</li> <li> **미디어 닫기로&#x200B;**<br/>전송</li> <li> **최소. SDK Version **<br/>3.0</li> <li> **샘플 값&#x200B;**<br/>TRUE</li><li> **설명&#x200B;**<br/>음소거를 선택한 시간입니다. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **중요** 이 이벤트가 설정되면 가능한 값만 TRUE입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatetime)<br/></li> <li> **하트비트&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **사용 가능&#x200B;**<br/>예</li> <li> **예약된 변수&#x200B;**<br/>이벤트</li> <li> **보고서 이름&#x200B;**<br/>음소거 기간</li> <li> **컨텍스트 데이터&#x200B;**<br/>(videostatetime)<br/> </li> <li> **데이터 피드&#x200B;**<br/>비디오 상태 시간</li> <li> **Audience Manager **<br/>(c_contextdata.videostatetime)</li> </ul> |


### 사진 속성의 그림


#### 그림의 영향을 받는 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키&#x200B;**<br/>자동 설정</li> <li> **API 키&#x200B;**<br/>해당 사항 없음</li> <li> **필수&#x200B;**<br/>아니오</li> <li> **문자&#x200B;**<br/>번호</li> <li> **미디어 닫기로&#x200B;**<br/>전송</li> <li> **최소. SDK Version **<br/>3.0</li> <li> **샘플 값&#x200B;**<br/>TRUE</li><li> **설명&#x200B;**<br/>그림 중 그림에서 영향을 받는 스트림의 수입니다. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **중요** 이 이벤트가 설정되면 가능한 값만 TRUE입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.pictureinpicture.set)<br/></li> <li> **하트비트&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **사용 가능&#x200B;**<br/>예</li> <li> **예약된 변수&#x200B;**<br/>이벤트</li> <li> **사진에서 사진이 영향을 받는 보고서 이름&#x200B;**<br/>스트림</li> <li> **컨텍스트 데이터&#x200B;**<br/>(a.media.states.pictureinpicture.set)<br/> </li> <li> **데이터 피드&#x200B;**<br/>videostacepictureinpicture</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.pictureinpicture.set)</li> </ul> |


#### 사진 수

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키&#x200B;**<br/>자동 설정</li> <li> **API 키&#x200B;**<br/>해당 사항 없음</li> <li> **필수&#x200B;**<br/>아니오</li> <li> **문자&#x200B;**<br/>번호</li> <li> **미디어 닫기로&#x200B;**<br/>전송</li> <li> **최소. SDK Version **<br/>3.0</li> <li> **샘플 값&#x200B;**<br/>TRUE</li><li> **설명&#x200B;**<br/>그림 내 그림이 표시된 횟수입니다. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **중요** 이 이벤트가 설정되면 가능한 값만 TRUE입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostacepicturepresentation)<br/></li> <li> **하트비트&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **사용 가능&#x200B;**<br/>예</li> <li> **예약된 변수&#x200B;**<br/>이벤트</li> <li> **사진 수의 보고서 이름&#x200B;**<br/>그림</li> <li> **컨텍스트 데이터&#x200B;**<br/>(videstacepicturepresentation)<br/> </li> <li> **데이터 피드&#x200B;**<br/>videostacepicturepresentation</li> <li> **Audience Manager **<br/>(c_contextdata.videostacepicturepresentation)</li> </ul> |


#### 그림 합계 기간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키&#x200B;**<br/>자동 설정</li> <li> **API 키&#x200B;**<br/>해당 사항 없음</li> <li> **필수&#x200B;**<br/>아니오</li> <li> **문자&#x200B;**<br/>번호</li> <li> **미디어 닫기로&#x200B;**<br/>전송</li> <li> **최소. SDK Version **<br/>3.0</li> <li> **샘플 값&#x200B;**<br/>TRUE</li><li> **설명&#x200B;**<br/>그림 내 시간 사진이 표시되었습니다. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **중요** 이 이벤트가 설정되면 가능한 값만 TRUE입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostacepicturetime)<br/></li> <li> **하트비트&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **사용 가능&#x200B;**<br/>예</li> <li> **예약된 변수&#x200B;**<br/>이벤트</li> <li> **그림 기간의 보고서 이름&#x200B;**<br/>그림</li> <li> **컨텍스트 데이터&#x200B;**<br/>(videostacepicturetime)<br/> </li> <li> **데이터 피드&#x200B;**<br/>videostacepicturetime</li> <li> **Audience Manager **<br/>(c_contextdata.videostacepicturetime)</li> </ul> |


### 초점 속성

#### 초점이 영향을 받는 스트림

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키&#x200B;**<br/>자동 설정</li> <li> **API 키&#x200B;**<br/>해당 사항 없음</li> <li> **필수&#x200B;**<br/>아니오</li> <li> **문자&#x200B;**<br/>번호</li> <li> **미디어 닫기로&#x200B;**<br/>전송</li> <li> **최소. SDK Version **<br/>3.0</li> <li> **샘플 값&#x200B;**<br/>TRUE</li><li> **설명&#x200B;**<br/>초점에 의해 영향을 받는 스트림 수입니다. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **중요** 이 이벤트가 설정되면 가능한 값만 TRUE입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.infocus.set)<br/></li> <li> **하트비트&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **사용 가능&#x200B;**<br/>예</li> <li> **예약된 변수&#x200B;**<br/>이벤트</li> <li> **초점이&#x200B;**<br/>영향을 받는 보고서 이름 스트림</li> <li> **컨텍스트 데이터&#x200B;**<br/>(a.media.states.infocus.set)<br/> </li> <li> **데이터 피드&#x200B;**<br/>videostateinfocus</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.infocus.set)</li> </ul> |


#### 초점 카운트

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키&#x200B;**<br/>자동 설정</li> <li> **API 키&#x200B;**<br/>해당 사항 없음</li> <li> **필수&#x200B;**<br/>아니오</li> <li> **문자&#x200B;**<br/>번호</li> <li> **미디어 닫기로&#x200B;**<br/>전송</li> <li> **최소. SDK Version **<br/>3.0</li> <li> **샘플 값&#x200B;**<br/>TRUE</li><li> **설명&#x200B;**<br/>포커스(In Focus)가 표시된 횟수입니다. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **중요** 이 이벤트가 설정되면 가능한 값만 TRUE입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateinfocuscount)<br/></li> <li> **하트비트&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **사용 가능&#x200B;**<br/>예</li> <li> **예약된 변수&#x200B;**<br/>이벤트</li> <li> **포커스&#x200B;**<br/>카운트의 보고서 이름</li> <li> **컨텍스트 데이터&#x200B;**<br/>(videostateinfocuscount)<br/> </li> <li> **데이터 피드&#x200B;**<br/>videostateinfocuscount</li> <li> **Audience Manager **<br/>(c_contextdata.videstateinfocuscount)</li> </ul> |


#### 초점 총 기간

|   구현   | 네트워크 매개 변수 | 보고 |
| --- | --- | --- |
| <ul> <li> **SDK 키&#x200B;**<br/>자동 설정</li> <li> **API 키&#x200B;**<br/>해당 사항 없음</li> <li> **필수&#x200B;**<br/>아니오</li> <li> **문자&#x200B;**<br/>번호</li> <li> **미디어 닫기로&#x200B;**<br/>전송</li> <li> **최소. SDK Version **<br/>3.0</li> <li> **샘플 값&#x200B;**<br/>TRUE</li><li> **설명&#x200B;**<br/>초점 중의 시간이 표시됩니다. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **중요** 이 이벤트가 설정되면 가능한 값만 TRUE입니다. 이 이벤트가 설정되지 않은 경우에는 값이 전송되지 않습니다.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateinfocustime)<br/></li> <li> **하트비트&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **사용 가능&#x200B;**<br/>예</li> <li> **예약된 변수&#x200B;**<br/>이벤트</li> <li> **포커스&#x200B;**<br/>기간의 보고서 이름</li> <li> **컨텍스트 데이터&#x200B;**<br/>(videostateinfocustime)<br/> </li> <li> **데이터 피드&#x200B;**<br/>videostateinfocustime</li> <li> **Audience Manager **<br/>(c_contextdata.videstateinfocustime)</li> </ul> |



## 관련 API {#related_apis_section}

필요: 문서에 API 링크 추가:
* Android - [createStateObject](https://need)
* iOS - [createStateObjectWithName](https://need)
* Javascript - [createStateObject](https://need)
