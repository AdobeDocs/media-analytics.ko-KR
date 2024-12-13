---
title: Adobe Experience Platform Web SDK을 사용하여 웹 데이터를 Edge으로 전송
description: Adobe Experience Platform Web SDK을 사용하여 Adobe 스트리밍 미디어 데이터를 Experience Platform Edge으로 전송하는 방법에 대해 알아봅니다.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: de40ebd9-46be-4a52-866f-7bb2589fce28
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Adobe Experience Platform Web SDK을 사용하여 웹 데이터를 Edge으로 전송

버전 2.20.0부터 Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)의 `streamingMedia` 구성 요소를 사용하여 웹 사이트에서 미디어 세션과 관련된 데이터를 수집할 수 있습니다. 수집된 데이터에는 미디어 재생, 일시 정지, 완료 및 기타 관련 이벤트에 대한 정보가 포함될 수 있습니다.

데이터가 수집되면 Adobe Experience Platform 및/또는 Adobe Analytics으로 전송하여 보고서를 생성할 수 있습니다. 이 기능은 웹 사이트에서의 미디어 소비 행동을 추적하고 이해하는 포괄적인 솔루션을 제공합니다.

Media JS SDK을 사용하는 고객을 위해 웹 SDK은 미디어 이벤트 처리와 같은 기존 Media JS 기능에 대한 지원을 포함하여 Media JS SDK에서 Web SDK으로 이동하는 마이그레이션 경로를 제공합니다.

## 사전 요구 사항 {#prerequisites}

Web SDK의 `streamingMedia` 구성 요소를 사용하려면 다음 사전 요구 사항을 충족해야 합니다.

* 스트리밍 미디어 데이터를 Edge으로 보내려면 먼저 [Experience Platform Edge으로 스트리밍 미디어 컬렉션 설치](/help/implementation/edge/implementation-edge.md)의 단계를 완료하십시오.
* Adobe Experience Platform 및/또는 Adobe Analytics에 액세스할 수 있는지 확인하십시오.
* 웹 SDK 버전 2.20.0 이상을 사용해야 합니다. 최신 버전을 설치하는 방법을 알아보려면 [웹 SDK 설치 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)를 참조하세요.
* 사용 중인 데이터 스트림에 대해 **[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)** 옵션을 사용하도록 설정하십시오.
* 데이터 스트림에서 사용하는 스키마에 미디어 컬렉션 스키마 필드가 포함되어 있는지 확인합니다.
* [태그 확장](#tag-extension) 또는 [JavaScript 라이브러리](#library)를 통해 이 페이지에 표시된 대로 웹 SDK 구성에서 스트리밍 미디어 기능을 구성합니다.

이 페이지에 설명된 단계에 따라 스트리밍 미디어 컬렉션 구현을 Media JS에서 Web SDK으로 마이그레이션합니다.

### 1단계: Experience Platform Web SDK 설치

웹 속성에 Web SDK을 설치하는 방법에 대해 알아보려면 [전용 설명서](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)를 참조하십시오.

### 2단계: 웹 SDK `streamingMedia` 구성 요소를 구성합니다.

**예**

아래 스니펫은 Media JS에서 미디어 컬렉션을 구성하는 방법을 보여 줍니다.

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

대신 아래 예제와 같이 웹 SDK에서 `streamingMedia` 구성 요소를 구성해야 합니다.

```js
alloy("configure", {
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

구성 방법에 대한 자세한 내용은 웹 SDK `streamingMedia` 구성 요소 [설명서](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/streamingmedia)를 참조하십시오.

### 3단계: Media JS SDK에서 마이그레이션할 때 미디어 추적기 인스턴스 가져오기

Media JS SDK을 사용하는 고객을 위해 웹 SDK은 미디어 이벤트 처리와 같은 기존 Media JS 기능에 대한 지원을 포함하여 Media JS SDK에서 Web SDK으로 이동하는 마이그레이션 경로를 제공합니다.

[!DNL Web SDK]에 Media Analytics 추적기를 검색하는 명령이 포함되어 있습니다. 이 명령을 사용하여 개체 인스턴스를 만든 다음 [Media JS 라이브러리](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)에서 제공한 것과 동일한 API를 사용하여 미디어 이벤트를 추적할 수 있습니다.

지원되는 메서드에 대한 자세한 내용은 [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker) 설명서를 참조하십시오.

아래 스니펫은 Media JS에서 미디어 추적기 인스턴스를 검색하는 방법을 보여 줍니다.

```javascript
var tracker = ADB.Media.getInstance();
```

대신 웹 SDK에서 `getMediaAnalyticsTracker` 명령을 사용하여 아래와 같이 동일한 결과를 얻습니다.

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

`Media` 개체에서 모든 도우미 메서드를 사용할 수 있습니다. 추적기 메서드는 아래와 같이 추적기 인스턴스에서 사용할 수 있습니다.

```js
const mediaInfo = Media.createMediaObject(
  "video name",
  "player video",
  60,
  Media.StreamType.VOD,
  Media.MediaType.Video
);

const contextData = {
  isUserLoggedIn: "false",
  tvStation: "Sample TV station",
  programmer: "Sample programmer",
  assetID: "/uri-reference"
};

// Set standard Video Metadata
contextData[Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[Media.VideoMetadataKeys.Show] = "Sample Show";

trackerInstance.trackSessionStart(mediaInfo, contextData);
```
