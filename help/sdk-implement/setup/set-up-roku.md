---
title: Roku용 Media SDK를 설정하는 방법
description: 다음 단계에 따라 Roku에서 Media SDK 애플리케이션을 설정합니다.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
exl-id: b8de88d0-3a93-4776-b372-736bf979ee26
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 78%

---

# Roku 설정{#set-up-roku}

## 전제 조건

* **하트비트에 대한 올바른 구성 매개 변수 가져오기**
이러한 매개 변수는 Media Analytics 계정을 설정한 후 Adobe 담당자에게서 얻을 수 있습니다.
* **미디어 플레이어에서 다음 기능 제공:**
   * _플레이어 이벤트에 가입할 API_ - Media SDK를 사용하려면 이벤트가 플레이어에서 발생할 때 단순 API 세트를 호출해야 합니다.
   * _플레이어 정보를 제공하는 API_ - 이 정보에는 미디어 이름 및 재생 헤드 위치와 같은 세부 정보가 포함됩니다.

Adobe Mobile Services는 Adobe Marketing Cloud에서 모바일 애플리케이션에 대한 모바일 마케팅 기능을 종합하여 제공하는 신규 UI를 제공합니다. 처음에, Mobile Service는 Adobe Analytics와 Adobe Target 솔루션의 앱 분석 및 타깃팅 기능을 매끄럽게 통합합니다.

자세한 내용은 [Adobe Mobile Services 문서](https://experienceleague.adobe.com/docs/mobile-services/using/home.html)에서 알아보십시오.

Experience Cloud 솔루션용 Roku SDK 2.x를 사용하여 BrightScript로 작성된 Roku 애플리케이션을 측정하고, 대상 관리를 통해 대상 데이터를 사용 및 수집하고, 비디오 하트비트를 통해 비디오 참여를 측정할 수 있습니다.

## SDK 구현

1. [다운로드한](/help/sdk-implement/download-sdks.md#download-2x-sdks) Roku 라이브러리를 프로젝트에 추가합니다.

   1. 다음 소프트웨어 구성 요소로 `AdobeMobileLibrary-2.*-Roku.zip` 다운로드 파일은 구성됩니다.

      * `adbmobile.brs`: 이 라이브러리 파일은 Roku 앱 소스 폴더에 포함됩니다.

      * `ADBMobileConfig.json`: 앱에 맞게 사용자 지정된 SDK 구성 파일입니다.
   1. 라이브러리 파일 및 json 구성 파일을 프로젝트 소스에 추가합니다.

      Adobe Mobile을 구성하는 데 사용되는 JSON에는 `mediaHeartbeat`라는 미디어 하트비트에 대한 배타 키가 있습니다. 여기에 미디어 하트비트에 대한 구성 매개 변수가 속해 있습니다.

      >[!TIP]
      >
      >샘플 `ADBMobileConfig` JSON 파일은 패키지와 함께 제공됩니다. 설정에 대해서는 Adobe 담당자에게 문의하십시오.

      예:

      ```
      {
        "version":"1.0",
        "analytics":{
          "rsids":"",
          "server":"",
          "charset":"UTF-8",
          "ssl":true,
          "offlineEnabled":false,
          "lifecycleTimeout":30,
          "batchLimit":50,
          "privacyDefault":"optedin",
          "poi":[ ]
      },
      "marketingCloud":{
        "org":""
      },
      "target":{
        "clientCode":"",
        "timeout":5
      },
      "audienceManager":{
        "server":""
      },
      "acquisition":{
        "server":"example.com",
        "appid":"sample-app-id"
      },
      
      "mediaHeartbeat":{
         "server":"example.com",
         "publisher":"sample-publisher",
         "channel":"sample-channel",
         "ssl":true,
         "ovp":"sample-ovp",
         "sdkVersion":"sample-sdk",
         "playerName":"roku"
         }    
      }
      ```

      | 구성 매개 변수 | 설명     |
      | --- | --- |
      | `server` | 백엔드에 대한 추적 끝점의 URL을 나타내는 문자열입니다. |
      | `publisher` | 컨텐츠 게시자 고유 식별자를 나타내는 문자열입니다. |
      | `channel` | 컨텐츠 배포 채널의 이름을 나타내는 문자열입니다. |
      | `ssl` | 추적 호출에 SSL을 사용해야 하는지 여부를 나타내는 부울입니다. |
      | `ovp` | 비디오 플레이어 공급자의 이름을 나타내는 문자열입니다. |
      | `sdkversion` | 앱/SDK의 현재 버전을 나타내는 문자열입니다. |
      | `playerName` | 플레이어의 이름을 나타내는 문자열입니다. |

      >[!IMPORTANT]
      >
      >`mediaHeartbeat`가 잘못 구성된 경우 미디어 모듈(VHL)이 오류 상태에 들어가고 추적 호출 전송을 중단합니다.


1. Experience Cloud 방문자 ID를 구성합니다.

   Experience Cloud 방문자 ID 서비스는 Experience Cloud 솔루션에 관계없이 유니버설 방문자 ID를 제공합니다. 방문자 ID 서비스는 비디오 하트비트 및 기타 Marketing Cloud 통합에 필요합니다.

   `ADBMobileConfig` 구성에 `marketingCloud` 조직 ID가 포함되어 있는지 확인합니다.

   ```
   "marketingCloud": {
       "org": YOUR-MCORG-ID"
   }
   ```

   Experience Cloud 조직 ID는 Adobe Marketing Cloud에서 각 고객 회사를 고유하게 식별하며, `016D5C175213CCA80A490D05@AdobeOrg` 값과 비슷하게 표시됩니다.

   >[!IMPORTANT]
   >
   >`@AdobeOrg`를 포함해야 합니다. 

   구성이 완료되면 Experience Cloud 방문자 ID가 생성되고, 모든 히트 수에 포함됩니다. 각 히트 수와 함께 `custom` 및 `automatically-generated` 같은 다른 방문자 ID는 계속 전송됩니다.

   **Experience Cloud 방문자 ID 서비스 메서드**

   >[!TIP]
   >
   >Experience Cloud 방문자 ID 메서드는 앞에 `visitor`가 붙습니다.

   |  메서드   | 설명 |
   | --- | --- |
   | `visitorMarketingCloudID` | 방문자 ID 서비스에서 Experience Cloud 방문자 ID를 검색합니다.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Experience Cloud 방문자 ID를 사용하면 각 방문자와 연결할 수 있는 추가 고객 ID를 설정할 수 있습니다. 방문자 API는 여러 다른 고객 ID의 범위를 구분하기 위해 동일한 방문자의 여러 고객 ID와 고객 유형 식별자를 허용합니다. 이 메서드는 `setCustomerIDs`에 해당합니다. 예: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | SDK에서 RIDA(Roku ID for Advertising)를 설정하는 데 사용됩니다. 예: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Roku SDK [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) API를 사용하여 RIDA(Roku ID for Advertising)를 가져옵니다. |
   | `getAllIdentifiers` | Analytics, 방문자, Audience Manager 및 사용자 지정 식별자를 포함하여 SDK에 저장된 모든 식별자 목록을 반환합니다.<br/><br/> `identifiers = ADBMobile().getAllIdentifiers()` |
   <!--
    Roku Api Reference:
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

   <br/><br/>

   **추가 공용 API**

   **DebugLogging**
| 메서드   | 설명 | | — | — | |  `setDebugLogging` | SDK에 대한 디버그 로깅을 활성화 또는 비활성화하는 데 사용됩니다.  <br/><br/>`ADBMobile().setDebugLogging(true)` | |  `getDebugLogging` | 디버그 로깅이 활성화되면 true를 반환합니다.   <br/><br/>`isDebugLoggingEnabled = ADBMobile().getDebugLogging()` |

   <br/><br/>

   **PrivacyStatus**
| 상수   | 설명 | | — | — | |  `PRIVACY_STATUS_OPT_IN` | setPrivacyStatus를 옵트인으로 호출하는 동안 전달할 상수. <br/><br/>`optInString = ADBMobile().PRIVACY_STATUS_OPT_IN`| |  `PRIVACY_STATUS_OPT_OUT` | 옵트아웃하도록 setPrivacyStatus를 호출하는 동안 전달할 상수.  <br/><br/>`optOutString = ADBMobile().PRIVACY_STATUS_OPT_OUT`|

   <br/>

   |  메서드   | 설명 |
   | --- | --- |
   | `setPrivacyStatus` | SDK에 대한 개인 정보 상태를 설정합니다. <br/><br/>`ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)` |
   | `getPrivacyStatus` | SDK에 설정된 현재 개인 정보 상태를 가져옵니다. <br/><br/>`privacyStatus = ADBMobile().getPrivacyStatus()` |

   <br/><br/>
   >[!IMPORTANT]
   >
   >250밀리초마다 기본 이벤트 루프에서 `processMessages` 및 `processMediaMessages` 함수를 호출하여 SDK가 Ping을 제대로 전송하는지 확인합니다.

   |  메서드   | 설명 |
   | --- | --- |
   | `processMessages` | 처리할 SDK에 Analytics 이벤트를 전달할 책임이 있습니다. <br/><br/>`ADBMobile().processMessages()` |
   | `processMediaMessages` | 처리할 SDK에 미디어 이벤트를 전달할 책임이 있습니다.<br/><br/>`ADBMobile().processMediaMessages()` |


<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
