---
title: JavaScript 2.x를 사용하여 미디어 SDK를 설정하는 방법
description: JavaScript 2.x에서 미디어 SDK 애플리케이션을 설정하려면 다음 단계를 따르십시오.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
exl-id: 33976096-8b86-4353-906b-e25bf4693471
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 96%

---

# JavaScript 2.x 설정{#set-up-javascript}

## 전제 조건

* **올바른 구성 매개 변수 가져오기** 이러한 매개 변수는 Analytics 계정을 설정한 후 Adobe 담당자에게서 얻을 수 있습니다.
* **미디어 애플리케이션에서 JavaScript용 `AppMeasurement` 구현**
Adobe Mobile SDK 설명서에 대한 자세한 내용은 [JavaScript를 사용하여 분석 구현](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=ko-KR)을 참조하십시오.

* **미디어 플레이어에서 다음 기능 제공:**

   * *플레이어 이벤트에 가입할 API* - Media SDK를 사용하려면 이벤트가 플레이어에서 발생할 때 단순 API 세트를 호출해야 합니다.
   * *플레이어 정보를 제공하는 API* - 이 정보에는 미디어 이름 및 재생 헤드 위치와 같은 세부 정보가 포함됩니다.

1. [다운로드한](/help/getting-started/download-sdks.md) 라이브러리를 프로젝트에 추가합니다. 편의상 클래스에 대한 로컬 참조를 작성하십시오.

   1. 다운로드한 `MediaSDK-js-v2.*.zip` 파일을 확장합니다.
   1. `MediaSDK.min.js` 파일이 `libs` 디렉토리에 있는지 확인합니다.

   1. `MediaSDK.min.js` 파일을 호스팅합니다.

      이 코어 JavaScript 파일은 사이트의 모든 페이지에 액세스할 수 있는 웹 서버에 호스팅해야 합니다. 다음 단계를 위해 이 파일에 대한 경로가 필요합니다.

   1. 모든 사이트 페이지에서 `MediaSDK.min.js`를 참조합니다.

      다음 코드 행을 각 페이지의 `MediaSDK` 또는 `<head>` 태그에 추가하여 JavaScript용 `<body>`를 포함합니다. 예:

      ```
      <script type="text/javascript"
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1.  라이브러리를 성공적으로 가져왔는지 확인하려면 `ADB.va.MediaHeartbeatConfig` 클래스를 인스턴스화합니다.

      >[!NOTE]
      >
      >버전 2.1.0부터 JavaScript SDK는 AMD 및 CommonJS 모듈 사양과 호환되며, `VideoHeartbeat.min.js`를 호환 가능한 모듈 로더와 함께 사용할 수도 있습니다.

1. API에 쉽게 액세스하기 위해 `MediaHeartbeat` 클래스에 대한 로컬 참조를 생성합니다.

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   ```

1. `MediaHeartbeatConfig` 인스턴스를 만듭니다.

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

1. `MediaHeartbeatDelegate` 프로토콜을 구현합니다.

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

1. `MediaHeartbeat` 인스턴스를 생성합니다.

   `MediaHeartbeatConfig` 및 `MediaHeartbeatDelegate`를 사용하여 `MediaHeartbeat` 인스턴스를 생성합니다.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >미디어 세션이 끝날 때까지 이 인스턴스에 대한 할당이 취소되지 않는지 그리고 `MediaHeartbeat` 인스턴스가 액세스할 수 있는지 확인하십시오. 이 인스턴스는 다음의 모든 추적 이벤트에 사용됩니다.

   >[!TIP]
   >
   >Adobe Analytics에 대한 호출을 전송하려면 `MediaHeartbeat`에 `AppMeasurement`의 인스턴스가 필요합니다. 다음은 `AppMeasurement` 인스턴스의 예제입니다.

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   appMeasurement.account = <rsid>;
   appMeasurement.pageName = <page_name>;
   appMeasurement.charSet = "UTF­8";
   ```

## JavaScript 1.x에서 2.x로 마이그레이션

버전 2.x에서 모든 공개 메서드는 개발자가 쉽게 만들 수 있도록 `ADB.va.MediaHeartbeat` 클래스에 통합되어 있습니다. 또한 모든 구성이 이제 `ADB.va.MediaHeartbeatConfig` 클래스에 통합되어 있습니다.

1.x에서 2.x로 마이그레이션에 대한 자세한 내용은 이전 구현 설명서를 참조하십시오.
