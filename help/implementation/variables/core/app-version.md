---
title: 앱 버전
description: 미디어 플레이어 애플리케이션의 버전 문자열을 구성합니다.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 2%

---


# 앱 버전

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**앱 버전**변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [앱 버전](/help/reporting/dimensions/app-version.md)을 참조하세요.*

>[!ENDSHADEBOX]

앱 버전 변수는 미디어 플레이어 애플리케이션의 버전을 식별합니다. SDK 초기화 중에 한 번 설정합니다. 이 값은 모든 후속 세션 시작 요청에 자동으로 포함됩니다. 응용 프로그램의 릴리스 주기(예: `"2.1.0"` 또는 `"prod-YYYY-03-15"`)와 일치하는 버전 문자열을 사용합니다.

>[!NOTE]
>
>이 필드는 Adobe의 SDK 라이브러리가 아닌 **미디어 플레이어 응용 프로그램**&#x200B;의 버전을 캡처합니다. Adobe의 자체 SDK 라이브러리 버전은 별도의 내부 필드로 자동으로 수집됩니다.

| 속성 | 값 |
| --- | --- |
| **XDM 컬렉션 필드** | [`xdm.mediaCollection.sessionDetails.appVersion`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **미디어 컬렉션 API 매개 변수** | `media.sdkVersion` |
| **필수** | 아니요 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md) |

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

[`configure`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/streamingmedia)을(를) 호출할 때 `streamingMedia` 구성 개체에 `appVersion`을(를) 설정합니다.

```javascript
alloy("configure", {
  streamingMedia: {
    channel: "Sports Channel",
    playerName: "HTML5 Player",
    appVersion: "2.1.0",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

>[!TAB iOS]

미디어 추적기를 초기화하기 전에 앱 구성에서 `edgeMedia.appVersion`을(를) 설정합니다.

```swift
var config: [String: Any] = [:]
config["edgeMedia.channel"] = "sample_channel"
config["edgeMedia.playerName"] = "player_name"
config["edgeMedia.appVersion"] = "2.1.0"
MobileCore.updateConfiguration(config)
```

>[!TAB Android]

미디어 추적기를 초기화하기 전에 앱 구성에서 `edgeMedia.appVersion`을(를) 설정합니다.

```kotlin
val config: Map<String, Any> = mapOf(
    "edgeMedia.channel" to "sample_channel",
    "edgeMedia.playerName" to "player_name",
    "edgeMedia.appVersion" to "2.1.0"
)
MobileCore.updateConfiguration(config)
```

>[!TAB Roku]

`ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION`을(를) 사용하여 SDK 구성에서 앱 버전을 설정합니다.

```brightscript
ADB_CONSTANTS = AdobeAEPSDKConstants()
configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<YOUR_CONFIG_ID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "channel_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION] = "2.1.0"
m.aepSdk.updateConfiguration(configuration)
```

>[!TAB 미디어 Edge API]

[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 요청의 `sessionDetails` 개체에 `appVersion` 포함:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 300,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "appVersion": "2.1.0"
        },
        "playhead": 0
      }
    }
  }]
}
```

>[!ENDTABS]

## 이전 구현 유형(Analytics 전용)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

`ADB.Media.configure`을(를) 호출하기 전에 `MediaConfig` 개체에 `appVersion`을(를) 설정합니다.

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "2.1.0";
ADB.Media.configure(mediaConfig, appMeasurement);
```

>[!TAB Chromecast]

ADBMobile 구성의 `mediaHeartbeat` 섹션에서 `sdkVersion`을(를) 설정합니다. 이 필드는 Chromecast SDK 라이브러리 버전이 아닌 플레이어 애플리케이션 버전을 캡처합니다.

```javascript
var ADBMobileConfig = {
  "mediaHeartbeat": {
    "server": "obumobile5.hb-api.omtrdc.net",
    "publisher": "<YOUR_PUBLISHER_ID>@AdobeOrg",
    "channel": "sample-channel",
    "ssl": true,
    "playerName": "Chromecast Player",
    "sdkVersion": "2.1.0"
  }
};
```

>[!TAB 미디어 컬렉션 API]

`sessionStart` POST 요청의 `params` 개체에 `media.sdkVersion` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.playerName": "sample-html5-api-player",
    "media.sdkVersion": "2.1.0",
    "media.channel": "sample-channel"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.

>[!ENDTABS]
