---
seo-title: JavaScript 설정
title: JavaScript 설정
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# JavaScript 설정{#set-up-javascript}

## 전제 조건

* **Obtain valid configuration parameters**
These parameters can be obtained from an Adobe representative after you set up your analytics account.
* **미디어 애플리케이션에서`AppMeasurement`JavaScript 구현** Adobe Mobile SDK 설명서에 대한 자세한 내용은 JavaScript를 사용한 [분석 구현을 참조하십시오.](https://marketing.adobe.com/resources/help/en_US/sc/implement/js_implementation.html)

* **미디어 플레이어에 다음 기능을 제공합니다.**

   * *플레이어 이벤트에 가입할 API* - Media SDK를 사용하려면 이벤트가 플레이어에서 발생할 때 단순 API 세트를 호출해야 합니다.
   * *플레이어 정보를 제공하는 API* - 이 정보에는 미디어 이름 및 플레이헤드 위치와 같은 세부 사항이 포함되어 있습니다.

1. [다운로드한](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) 라이브러리를 프로젝트에 추가합니다. 편의상 클래스에 대한 로컬 참조를 작성하십시오.

   1. 다운로드한 `MediaSDK-js-v2.*.zip` 파일을 확장합니다.
   1. Verify that the `MediaSDK.min.js` file exists in the `libs` directory:

   1. Host the `MediaSDK.min.js` file.

      이 코어 JavaScript 파일은 사이트의 모든 페이지에 액세스할 수 있는 웹 서버에 호스팅해야 합니다. 다음 단계에서 이 파일에 대한 경로가 필요합니다.

   1. 모든 사이트 페이지에서 `MediaSDK.min.js`를 참조합니다.

      Include `MediaSDK` for JavaScript by adding the following line of code in the `<head>` or `<body>` tag on each page. 예:

      ```
      <script type="text/javascript" 
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1.  라이브러리를 성공적으로 가져왔는지 확인하려면 `ADB.va.MediaHeartbeatConfig` 클래스를 인스턴스화합니다.

      >[!NOTE]
      >
      >From Version 2.1.0, the JavaScript SDK is compliant with the AMD and CommonJS module specifications, and `VideoHeartbeat.min.js` can also be used with compatible module loaders.

1. API에 쉽게 액세스하기 위해 `MediaHeartbeat` 클래스에 대한 로컬 참조를 생성합니다.

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   ```

1. Create a `MediaHeartbeatConfig` instance.

   이 섹션은 `MediaHeartbeat` 구성 매개 변수를 이해하고, 정확한 추적을 위해 `MediaHeartbeat` 인스턴스에 올바른 구성 값을 설정하는 데 도움을 줍니다.

   다음은 샘플 `MediaHeartbeatConfig` 초기화입니다.

   ```js
   //Media Heartbeat initialization 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER; 
   mediaConfig.playerName = Configuration.PLAYER.NAME; 
   mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL; 
   mediaConfig.debugLogging = true; 
   mediaConfig.appVersion = Configuration.HEARTBEAT.SDK; 
   mediaConfig.ssl = false; 
   mediaConfig.ovp = Configuration.HEARTBEAT.OVP; 
   ```

1. Implement the `MediaHeartbeatDelegate` protocol.

   ```js
   var mediaDelegate = new MediaHeartbeatDelegate(); 
   
   // Replace <currentPlaybackTime> with the video player current playback time 
   mediaDelegate.getCurrentPlaybackTime = function() { 
       return <currentPlaybackTime>; 
   }; 
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.  
   mediaDelegate.getQoSObject = function() { 
       return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>); 
   };
   ```

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` and `MediaHeartbeatDelegate` to create the `MediaHeartbeat` instance.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the media session. 이 인스턴스는 다음의 모든 추적 이벤트에 사용됩니다.

   >[!TIP]
   >
   >`MediaHeartbeat` adobe Analytics에 호출을 `AppMeasurement` 전송하는 인스턴스가 필요합니다. 다음은 `AppMeasurement` 인스턴스의 예제입니다.

   ```js
   var appMeasurement = new AppMeasurement(); 
   appMeasurement.visitor = visitor; 
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net"; 
   appMeasurement.account = <rsid>; 
   appMeasurement.pageName = <page_name>; 
   appMeasurement.charSet = "UTF­8";
   ```

## JavaScript에서 버전 1.x에서 2.x로 마이그레이션

버전 2.x에서 모든 공개 메서드는 개발자가 쉽게 만들 수 있도록 `ADB.va.MediaHeartbeat` 클래스에 통합되어 있습니다. 또한 모든 구성이 이제 `ADB.va.MediaHeartbeatConfig` 클래스에 통합되어 있습니다.

For detailed information about migrating from 1.x to 2.x, see [VHL 1.x to 2.x Migration.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
