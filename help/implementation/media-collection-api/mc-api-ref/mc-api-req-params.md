---
title: 스트리밍 미디어 컬렉션 API - 요청 매개 변수
description: “미디어 컬렉션 API 요청 매개 변수, 요청 키 및 설명은 무엇입니까?”
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
exl-id: a70025ec-1418-46f1-b41f-433d09f024e1
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0079116bcf39bb6d20b4fd5f14bd3c19137c46e3
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 100%

---

# 요청 매개 변수{#request-parameters}

## 분석 데이터

| 요청 키  | 필수 여부 | 요청 유형 키 | 시작 시기... |  설명  |
| --- | :---: | :---: | :---: | --- |
| `analytics.trackingServer` | Y | 문자열 | `sessionStart` | Adobe Analytics 서버의 URL |
| `analytics.reportSuite` | Y | 문자열 | `sessionStart` | Analytics 보고 데이터를 식별하는 ID |
| `analytics.enableSSL` | N | 부울 | `sessionStart` | SSL을 사용할 True 또는 False |
| `analytics.visitorId` | N | 문자열 | `sessionStart` | Adobe 방문자 ID는 여러 Adobe 애플리케이션에서 사용할 수 있는 사용자 지정 ID입니다. 하트비트 `visitorId`는 Analytics `VID.`와 같습니다. |

## 방문자 데이터

| 요청 키  | 필수 여부 | 요청 유형 키 | 시작 시기... |  설명  |
| --- | :---: | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | 문자열 | `sessionStart` | Experience Cloud 조직 ID, Adobe Experience Cloud 관련 시스템 내에서 조직 식별 |
| `visitor.marketingCloudUserId` | N | 문자열 | `sessionStart` | ECID(Experience Cloud 사용자 ID)입니다. 대부분의 시나리오에서 사용자를 식별하는 데 사용해야 하는 ID입니다. 하트비트 `marketingCloudUserId`는 Adobe Analytics의 `MID`와 같습니다. 이 매개 변수는 기술적으로 필요하지 않지만, Experience Cloud 앱 제품군에 액세스하는 데 필요합니다. |
| `visitor.aamLocationHint` | N | 정수 | `sessionStart` | Adobe Audience Manager Edge 데이터 제공 - 값을 입력하지 않으면 값은 null입니다. |
| `appInstallationId` | N | 문자열 | `sessionStart` | appInstallationId가 앱 및 장치를 고유하게 식별함 |

## 콘텐츠 데이터

| 요청 키  | 필수 여부 | 요청 유형 키 | 시작 시기... |  설명  |
| --- | :---: | :---: | :---: | --- |
| `media.id` | Y | 문자열 | `sessionStart` | 콘텐츠에 대한 고유 식별자 |
| `media.name` | N | 문자열 | `sessionStart` | 사용자가 읽을 수 있는 콘텐츠 이름 |
| `media.length` | Y | 숫자 | `sessionStart` | 콘텐츠 길이(초) |
| `media.contentType` | Y | 문자열 | `sessionStart` | 스트림 형식(임의의 문자열일 수 있으며, &quot;Live&quot;, &quot;VOD&quot; 또는 &quot;Linear&quot; 값이 권장됨) |
| `media.playerName` | Y | 문자열 | `sessionStart` | 콘텐츠 렌더링을 담당하는 플레이어의 이름 |
| `media.channel` | Y | 문자열 | `sessionStart` | 콘텐츠 배포 채널. 모바일 애플리케이션 이름이나 웹 사이트 이름, 속성 이름일 수 있습니다. |
| `media.resume` | N | 부울 | `sessionStart` | 사용자가 이전 세션을 다시 시작하는지 여부를 나타냅니다(새 세션 시작과 반대됨). |
| `media.sdkVersion` | N | 문자열 | `sessionStart` | 플레이어에서 사용하는 SDK 버전 |

## 콘텐츠 표준 메타데이터

| 요청 키  | 필수 여부 | 요청 유형 키 | 시작 시기... |  설명  |
| --- | :---: | :---: | :---: | --- |
| `media.streamFormat` | N | 문자열 | `sessionStart` | 스트림 형식(예: “HD”) |
| `media.show` | N | 문자열 | `sessionStart` | 프로그램 또는 시리즈 이름 |
| `media.season` | N | 문자열 | `sessionStart` | 프로그램 또는 시리즈가 속한 시즌 번호 |
| `media.episode` | N | 문자열 | `sessionStart` | 에피소드의 번호 |
| `media.assetId` | N | 문자열 | `sessionStart` | TV 시리즈 에피소드 식별자, 동영상 자산 식별자 또는 라이브 이벤트 식별자와 같은 비디오 자산 콘텐츠에 대한 고유 식별자입니다. 일반적으로 이러한 ID는 EIDR, TMS/Gracenote 또는 Rovi와 같은 메타데이터 기관에서 나옵니다. 이러한 식별자는 다른 소유권 또는 사내 시스템에서도 사용할 수 있습니다. |
| `media.genre` | N | 문자열 | `sessionStart` | 콘텐츠 생성자에서 정의한 콘텐츠의 유형 |
| `media.firstAirDate` | N | 문자열 | `sessionStart` | 콘텐츠가 TV에 처음 방송된 날짜 |
| `media.firstDigitalDate` | N | 문자열 | `sessionStart` | 콘텐츠가 디지털 플랫폼에서 처음으로 방송된 날짜 |
| `media.rating` | N | 문자열 | `sessionStart` | TV 유해 콘텐츠 가이드라인으로 정의된 등급 |
| `media.originator` | N | 문자열 | `sessionStart` | 콘텐츠 작성자 |
| `media.network` | N | 문자열 | `sessionStart` | 네트워크/채널 이름 |
| `media.showType` | N | 문자열 | `sessionStart` | 0과 3 사이의 정수로 표시되는 콘텐츠의 유형입니다. <ul> <li>0 - 전체 에피소드 </li> <li>1 - 미리 보기 </li> <li>2 - 클립 </li> <li>3 - 기타 </li> </ul> |
| `media.adLoad` | N | 문자열 | `sessionStart` | 로드된 광고 유형 |
| `media.pass.mvpd` | N | 문자열 | `sessionStart` | Adobe 인증에서 제공한 MVPD |
| `media.pass.auth` | N | 문자열 | `sessionStart` | Adobe 인증을 통해 사용자가 인증되었음을 나타냄(설정된 경우에만 true일 수 있음) |
| `media.dayPart` | N | 문자열 | `sessionStart` | 콘텐츠가 브로드캐스트된 시간 |
| `media.feed` | N | 문자열 | `sessionStart` | 피드 유형(예: &quot;West-HD&quot;) |

## 광고 데이터

| 요청 키  | 필수 여부 | 요청 유형 키 | 시작 시기... |  설명  |
| --- | :---: | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | 문자열 | `adBreakStart` | 친숙한 광고 브레이크 이름 |
| `media.ad.podIndex` | Y | 정수 | `adBreakStart` | 비디오에 있는 광고 pod 인덱스 |
| `media.ad.podSecond` | Y | 숫자 | `adBreakStart` | pod가 시작된 시간(초) |
| `media.ad.podPosition` | Y | 정수 | `adStart` | 광고 브레이크 내에 있는 광고 인덱스(1부터 시작) |
| `media.ad.name` | N | 문자열 | `adStart` | 친숙한 광고 이름 |
| `media.ad.id` | Y | 문자열 | `adStart` | 광고 이름 |
| `media.ad.length` | Y | 숫자 | `adStart` | 비디오 광고 길이(초) |
| `media.ad.playerName` | Y | 문자열 | `adStart` | 광고를 렌더링하는 플레이어의 이름 |

## 광고 표준 메타데이터

| 요청 키  | 필수 여부 | 요청 유형 키 | 시작 시기... |  설명  |
| --- | :---: | :---: | :---: | --- |
| `media.ad.advertiser` | N | 문자열 | `adStart` | 광고에서 다루고 있는 제품의 회사 또는 브랜드입니다 |
| `media.ad.campaignId` | N | 문자열 | `adStart` | 광고 캠페인의 ID |
| `media.ad.creativeId` | N | 문자열 | `adStart` | 광고 문안 ID |
| `media.ad.siteId` | N | 문자열 | `adStart` | 광고 사이트의 ID |
| `media.ad.creativeURL` | N | 문자열 | `adStart` | 광고 문안 URL |
| `media.ad.placementId` | N | 문자열 | `adStart` | 광고 배치 ID |

## 챕터 데이터

| 요청 키  | 필수 여부 | 요청 유형 키 | 시작 시기... |  설명  |
| --- | :---: | :---: | :---: | --- |
| `media.chapter.index` | Y | 정수 | `chapterStart` | 콘텐츠에서 챕터의 위치 식별 |
| `media.chapter.offset` | Y | 숫자 | `chapterStart` | 재생에서 챕터가 시작되는 시간(초) |
| `media.chapter.length` | Y | 숫자 | `chapterStart` | 챕터의 길이(초) |
| `media.chapter.friendlyName` | N | 문자열 | `chapterStart` | 친숙한 챕터 이름 |

## 품질 데이터

| 요청 키  | 필수 여부 | 요청 유형 키 | 시작 시기... |  설명  |
| --- | :---: | :---: | :---: | --- |
| `media.qoe.bitrate` | N | 정수 | 임의 | 평균 비트율(bps)입니다. 평균 비트율은 재생 기간과 관련하여 재생 세션 중에 발생한 모든 비트율 값의 가중 평균으로. |
| `media.qoe.droppedFrames` | N | 정수 | 임의 | 스트림의 드롭된 프레임 수 |
| `media.qoe.framesPerSecond` | N | 정수 | 임의 | 초당 프레임 수 |
| `media.qoe.timeToStart` | N | 정수 | 임의 | 사용자가 재생을 누르는 때와 콘텐츠가 로드되어 재생을 시작할 때 사이에 경과된 시간(밀리초)입니다. |

## CCPA(California Consumer Privacy Act) 매개 변수 {#ccpa-params}

| 요청 키  | 필수 여부 | 요청 유형 키 | 시작 시기... |  설명  |
| --- | :---: | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | N | 부울 | `sessionStart` | 최종 사용자가 Adobe Analytics와 다른 Experience Cloud 솔루션(예: Audience Manager) 간에 데이터를 공유하지 않기로 선택한 경우 참으로 설정합니다. |
| `analytics.optOutShare` | N | 부울 | `sessionStart` | 최종 사용자가 데이터를 (예: 다른 Adobe Analytics 클라이언트로) 페더레이션하지 않기로 선택한 경우 참으로 설정합니다. |

## 추가 세부 정보 {#additional-details}

### visitor.marketingCloudUserId

맵 `params` 내부에 Experience Cloud 사용자 ID(`MID` 또는 `MCID`라고도 함)를 포함하면 **visitor.marketingCloudUserId** 키를 사용하여 `sessionStart` 호출 시 Experience Cloud 사용자 ID를 전달합니다. 이 기능은 다른 Experience Cloud 제품과 이미 통합하고 MCID를 가져온 경우에 유용합니다.

>[!NOTE]
>
>MA(Media Analytics)는 Experience Cloud 앱 제품군(Adobe Analytics, Audience Manager, Target 등)에 통합되어 있습니다. 이러한 앱에 액세스하려면 Experience Cloud ID가 필요합니다. _ECID는 대부분의 시나리오에서 사용자를 식별하는 데 사용해야 하는 것입니다._

### appInstallationId

* **`appInstallationId` 값을 전달하지 *않은 경우* -** MA 백 엔드가 더 이상 MCID를 생성하지 않고, Adobe Analytics를 대신 이용하여 이 작업을 수행합니다. Media Collection API에서 MCID를 생성하여 모든 요청 시 보낼 수 있도록 가능한 경우 MCID를 보내거나 `appInstallationId`(필수 `marketingCloudOrgId`와 함께 사용)를 보내는 것이 좋습니다.

* **`appInstallationId` 값을 전달&#x200B;*하는* 경우 -** `appInstallationId` 및 (필수) `marketingCloudOrgId` 매개 변수 값을 전달하는 경우 MA 백 엔드에서 MCID를 생성&#x200B;*할 수 있습니다*. `appInstallationId`를 직접 전달하는 경우 클라이언트 측에서 해당 값을 유지해야 합니다. 이는 장치의 앱에 고유해야 하며, 앱이 다시 설치되지 않는 한 유지되어야 합니다.

>[!NOTE]
>
>`appInstallationId`는 앱 및 *장치*&#x200B;를 고유하게 식별합니다. 각 장치의 각 앱에 대해 고유해야 합니다. 즉, 다른 장치에서 동일한 앱의 동일한 버전을 사용하는 두 명의 사용자가 각각 다른(고유) `appInstallationId`를 보내야 합니다.

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The .
\<ul id="ul_iwc_fqt_pbb"\>
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li>
</ul> -->

### visitor.marketingCloudOrgId

이 매개 변수는 제공하지 않은 경우 MCID 생성에 필요하며, 게시자 ID(Media Analytics에서 [페더레이션 규칙 일치](/help/use-cases/federated-media.md)를 수행할 때 기반으로 함)에 대한 값으로도 사용됩니다.

### Analytics 기존 사용 ID(aid) 및 선언된 사용자 ID(customerIDs)

* **analytics.aid:**

  이 키 값은 Analytics 기존 사용자 ID를 나타내는 문자열이어야 합니다.
* **visitor.customerIDs:**

  이 키의 값은 다음 형식의 개체여야 합니다.

  ```js
  "<<insert your ID name here>>": {  
    "id": " <<insert your id here>>",  
     "authState": <<insert one of 0, 1, 2>>
  }
  ```

`visitor.customerIDs` 값은 제공된 형식의 개체를 임의의 수만큼 가질 수 있습니다.

### visitor.aamLocationHint

이 매개 변수는 Adobe Analytics에서 고객 데이터를 Audience Manager에게 보낼 때 AAM(Adobe Audience Manager) Edge가 적중됨을 나타냅니다. 값을 입력하지 않으면 값은 null입니다. 이는 최종 사용자가 지리적으로 먼 곳(예: 미국-동부, 미국-서부, 유럽, 아시아)에서 장치를 사용하는 경향이 있는 경우에 특히 중요합니다. 다른 경우에는 사용자 데이터가 여러 AAM Edges에 분산됩니다.

### media.resume

세션이 닫히고 나중에 재개되었다고 판단되면(예: 사용자가 비디오를 나갔지만 결국 다시 플레이어에서 비디오가 중단된 플레이헤드부터 비디오를 재개한 경우) **호출 시 params 버킷 내에 선택적 부울** media.resume`sessionStart` 매개 변수를 보낼 수 있습니다.

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
