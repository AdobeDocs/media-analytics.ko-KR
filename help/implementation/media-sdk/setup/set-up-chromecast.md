---
title: Chromecast용 Media SDK를 설정하는 방법
description: Chromecast에서 Media SDK 애플리케이션을 설정하려면 다음 단계를 따르십시오.
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
exl-id: 5dfe3407-2858-48c0-a70c-8ea87967ac47
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 97%

---

# Chromecast용 Mobile SDK v3.x 설정 {#set-up-chromecast}

이 섹션에서는 스트리밍 미디어 컬렉션 추가 기능에 대한 Chromecast 설치를 설정하기 위한 사전 요구 사항을 설명합니다.

## 사전 요구 사항

* **유효한 구성 매개 변수 얻기**

  이러한 매개 변수는 미디어 분석 계정을 설정한 후에 Adobe 담당자로부터 얻을 수 있습니다.
* **미디어 플레이어에서 다음 API 포함**

   * *플레이어 이벤트에 가입할 API* - Media SDK를 사용하려면 이벤트가 플레이어에서 발생할 때 단순 API 세트를 호출해야 합니다.
   * *플레이어 정보를 제공하는 API* - 이 정보에는 미디어 이름 및 재생 헤드 위치와 같은 세부 정보가 포함됩니다.

Adobe Mobile Services는 Adobe Marketing Cloud에서 모바일 애플리케이션에 대한 모바일 마케팅 기능을 종합하여 제공하는 신규 UI를 제공합니다. 처음에, Mobile Service는 Adobe Analytics와 Adobe Target 솔루션의 앱 분석 및 타깃팅 기능을 매끄럽게 통합합니다. 자세한 내용은 [Adobe Mobile Services 문서](https://experienceleague.adobe.com/docs/mobile-services/using/home.html)에서 알아보십시오.

Experience Cloud 솔루션용 Chromecast v3.x의 Adobe 모바일 라이브러리를 사용하여 JavaScript로 작성된 Chromecast 애플리케이션을 측정하고, 고객 관리를 통해 대상자 데이터를 활용 및 수집하고, 비디오 참여를 측정할 수 있습니다.

## 모바일 라이브러리 / SDK 구현

1. 다운로드한 Chromecast 라이브러리를 프로젝트에 추가합니다.

   1. `AdobeMobileLibrary-Chromecast-[version]`.zip 파일은 다음 소프트웨어 구성 요소로 구성됩니다.

      * `adbmobile-chromecast.min.js`:

        이 라이브러리 파일은 Chromecast 앱 소스 폴더에 포함됩니다.

      * `ADBMobileConfig` 구성

        앱에 맞게 사용자 지정된 SDK 구성 파일입니다. 샘플 `ADBMobileConfig` 구현은 SDK(`samples/` / 아래)와 함께 제공됩니다. Adobe 담당자로부터 적절한 설정을 확보하십시오.

   1. 라이브러리 파일을 `index.html` 파일에 추가하고 `ADBMobileConfig` 전역 변수를 생성하십시오(Media Analytics용 Adobe Mobile을 구성하는 데 사용되는 전역 변수에는 `mediaHeartbeat`라는 배타적 키가 있음).

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
              "rsids": "example.sample.player",
              "server": "example.sc.omtrc.net",
              "ssl": true,
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
              "server": "example.hb-api.omtrdc.net",
              "publisher": "972C898555E9F7BC7F000101@AdobeOrg",
              "channel": "test-channel-chromecast",
              "ssl": true,
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
      >`mediaHeartbeat`가 잘못 구성된 경우, 미디어 모듈은 오류 상태에 들어가고 추적 호출 전송을 중단합니다.

      mediaHeartbeat 키에 대한 ADBMobile 구성 매개 변수:

   | 구성 매개 변수 | 설명     |
   | --- | --- |
   | `server` | 백엔드에 대한 추적 엔드포인트의 URL을 나타내는 문자열입니다. |
   | `publisher` | 콘텐츠 게시자 고유 식별자를 나타내는 문자열입니다. |
   | `channel` | 콘텐츠 배포 채널의 이름을 나타내는 문자열입니다. |
   | `ssl` | 추적 호출에 SSL을 사용해야 하는지 여부를 나타내는 부울입니다. |
   | `ovp` | 비디오 플레이어 공급자의 이름을 나타내는 문자열입니다. |
   | `sdkversion` | 앱/SDK의 현재 버전을 나타내는 문자열입니다. |
   | `playerName` | 플레이어의 이름을 나타내는 문자열입니다. |


1. Experience Cloud 방문자 ID를 구성합니다.

   Experience Cloud 방문자 ID 서비스는 Experience Cloud 솔루션에 관계없이 유니버설 방문자 ID를 제공합니다. 방문자 ID 서비스는 Media Analytics 및 다른 Marketing Cloud 통합에 필요합니다.

   `ADBMobileConfig` 구성에 `marketingCloud` 조직 ID가 포함되어 있는지 확인합니다.

   ```
   "marketingCloud": {
       "org": "YOUR-MCORG-ID"
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

   | 메서드 | 설명 |
   | --- | --- |
   | `getMarketingCloudID()` | 방문자 ID 서비스에서 Experience Cloud 방문자 ID를 검색합니다.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Experience Cloud 방문자 ID를 사용하면 각 방문자와 연결할 수 있는 추가 고객 ID를 설정할 수 있습니다. 방문자 API는 여러 다른 고객 ID의 범위를 구분하기 위해 동일한 방문자의 여러 고객 ID와 고객 유형 식별자를 허용합니다. 이 메서드는 JavaScript 라이브러리의 `setCustomerIDs()`에 해당합니다.  예: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |

1. 미디어 추적을 위해 MediaDelegate 프로토콜 구현

   ```js
    var delegate = {
      // Replace <currentPlaybackTime> with the video player current playback time
      getCurrentPlaybackTime = function() {
        return <currentPlaybackTime>;
      },
      // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.
      getQoSObject = function() {
         return ADBMobile.media.createQoSObject(<bitrate>, <startupTime>, <fps>, <droppedFrames>);
      }
    }
   
    ADBMobile.media.setDelegate(delegate);
   }
   ```

<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
