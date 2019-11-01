---
title: Chromecast 설정
description: Chromecast 구현을 위한 미디어 SDK 애플리케이션 설정
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Chromecast 설정{#set-up-chromecast}

## FAQ

_Chromecast JavaScript SDK를 사용해야 합니까, 아니면 표준 JavaScript SDK를 사용할 수 있습니까?_

다음의 이유로 정답은 "크로메캐스트"입니다.
* 표준 JS SDK의 AppMeasurement 및 VisitorAPI 라이브러리는 OTT 플랫폼에서 작동하는 것으로 인증되지 않았습니다. Chromecast JS SDK에서는 비디오 하트비트 라이브러리(VHL), Analytics 및 VisitorAPI가 모두 통합 및 Chromecast용으로 인증된 하나의 SDK에 내장되어 있습니다.
* Chromecast SDK는 표준 JS SDK보다 훨씬 간단합니다. 이것은 OTT 플랫폼에서 사용하는 하단 하드웨어에 매우 중요합니다.

## 전제 조건

* **하트비트에 대한 유효한 구성 매개 변수**&#x200B;얻기 미디어 분석 계정을 설정한 후 Adobe 담당자로부터 이러한 매개 변수를 얻을 수 있습니다.
* **미디어 플레이어에 다음 기능을 제공합니다.**
   * *플레이어 이벤트에 가입할 API* - Media SDK를 사용하려면 이벤트가 플레이어에서 발생할 때 단순 API 세트를 호출해야 합니다.
   * *플레이어 정보를 제공하는 API* - 이 정보에는 미디어 이름 및 플레이헤드 위치와 같은 세부 사항이 포함되어 있습니다.

Adobe Mobile Services는 Adobe Marketing Cloud에서 모바일 애플리케이션에 대한 모바일 마케팅 기능을 종합하여 제공하는 신규 UI를 제공합니다. 처음에, Mobile Service는 Adobe Analytics와 Adobe Target 솔루션의 앱 분석 및 타깃팅 기능을 매끄럽게 통합합니다. Learn more at [Adobe Mobile Services documentation.](https://marketing.adobe.com/resources/help/en_US/mobile/)

Experience Cloud 솔루션용 Chromecast SDK 2.x를 사용하여 JavaScript로 작성된 Chromecast 애플리케이션을 측정하고, 대상 관리를 통해 대상 데이터를 활용 및 수집하고, 비디오 하트비트를 통해 비디오 참여를 측정할 수 있습니다.

## SDK 구현

1. [다운로드한](/help/sdk-implement/download-sdks.md#download-2x-sdks) Chromecast 라이브러리를 프로젝트에 추가합니다.

   1. `AdobeMobileLibrary-Chromecast-[version]`.zip 파일은 다음 소프트웨어 구성 요소로 구성됩니다.

      * `adbmobile-chromecast.min.js`:

         이 라이브러리 파일은 Chromecast 앱 소스 폴더에 포함됩니다.

      * `ADBMobileConfig` config

         앱에 맞게 사용자 지정된 SDK 구성 파일입니다. 샘플 `ADBMobileConfig` 구현은 SDK(`samples/` / 아래)와 함께 제공됩니다. Adobe 담당자로부터 적절한 설정을 확보하십시오.
   1. 라이브러리 파일을 `index.html` 파일에 추가하고 `ADBMobileConfig` 전역 변수를 생성하십시오(Adobe Mobile for Heartbeats를 구성하는 데 사용되는 전역 변수에는 `mediaHeartbeat`라는 배타적 키가 있습니다.).

      ```js
      <script> 
          var ADBMobileConfig = { 
            "marketingCloud": { 
              "org": "972C898555E9F7BC7F000101@AdobeOrg" 
            }, 
            "target": { 
              "clientCode": "", 
              "timeout": 5 
            }, 
            "audienceManager": { 
              "server": "obumobile5.demdex.net" 
            }, 
            "analytics": { 
              "rsids": "mobile5vhl.sample.player", 
              "server": "obumobile5.sc.omtrdc.net", 
              "ssl": false, 
              "offlineEnabled": false, 
              "charset": "UTF-8", 
              "lifecycleTimeout": 300, 
              "privacyDefault": "optedin", 
              "batchLimit": 0, 
              "timezone": "MDT", 
              "timezoneOffset": -360, 
              "referrerTimeout": 0, 
              "poi": [] 
            }, 
            "mediaHeartbeat": { 
              "server": "obumobile5.hb.omtrdc.net", 
              "publisher": "972C898555E9F7BC7F000101@AdobeOrg", 
              "channel": "test-channel-chromecast", 
              "ssl": false, 
              "ovp": "chromecast-player", 
              "sdkVersion": "chromecast-sdk", 
              "playerName": "Chromecast" 
            } 
          }; 
        </script> 
      <script type="text/javascript" src="script/lib/adbmobile-chromecast.min.js"></script>
      ```

      >[!IMPORTANT]
      >
      >If `mediaHeartbeat` is incorrectly configured, the media module (VHL) enters an error state and will stop sending tracking calls.

      mediaHeartbeat 키에 대한 ADBMobile 구성 매개 변수:
   | 구성 매개 변수 | 설명     |
   | --- | --- |
   | `server` | 백엔드에 대한 추적 끝점의 URL을 나타내는 문자열입니다. |
   | `publisher` | 컨텐츠 게시자 고유 식별자를 나타내는 문자열입니다. |
   | `channel` | 컨텐츠 배포 채널의 이름을 나타내는 문자열입니다. |
   | `ssl` | 추적 호출에 SSL을 사용해야 하는지 여부를 나타내는 부울입니다. |
   | `ovp` | 비디오 플레이어 공급자의 이름을 나타내는 문자열입니다. |
   | `sdkversion` | 앱/SDK의 현재 버전을 나타내는 문자열입니다. |
   | `playerName` | 플레이어의 이름을 나타내는 문자열입니다. |


1. Experience Cloud 방문자 ID를 구성합니다.

   Experience Cloud 방문자 ID 서비스는 Experience Cloud 솔루션 전반에 유니버설 방문자 ID를 제공합니다. 방문자 ID 서비스는 비디오 하트비트 및 다른 Marketing Cloud 통합에 필요합니다.

   Verify that your `ADBMobileConfig` config contains your `marketingCloud` organization ID.

   ```js
   "marketingCloud": { 
       "org": YOUR-MCORG-ID" 
   }
   ```

   Experience Cloud organization IDs uniquely identify each client company in the Adobe Marketing Cloud and appear similar to the following value: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Ensure that you include `@AdobeOrg`.

   구성이 완료되면 Experience Cloud 방문자 ID가 생성되고, 모든 히트 수에 포함됩니다. Other Visitor IDs, such as `custom` and `automatically-generated`, continue to be sent with each hit.

   **Experience Cloud 방문자 ID 서비스 메서드**

   >[!TIP]
   >
   >Experience Cloud Visitor ID methods are prefixed with `visitor`.

   | 메서드 | 설명 |
   | --- | --- |
   | `getMarketingCloudID()` | 방문자 ID 서비스에서 Experience Cloud 방문자 ID를 검색합니다.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Experience Cloud 방문자 ID를 사용하면 각 방문자와 연결할 수 있는 추가 고객 ID를 설정할 수 있습니다. 방문자 API는 여러 다른 고객 ID의 범위를 구분하기 위해 동일한 방문자의 여러 고객 ID와 고객 유형 식별자를 허용합니다. 이 메서드는 JavaScript 라이브러리의 `setCustomerIDs()`에 해당합니다.  For example: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |


<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html) -->

