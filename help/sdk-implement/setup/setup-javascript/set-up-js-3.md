---
title: JavaScript 3.x 설정
description: JavaScript 3.x에서 구현을 위한 미디어 SDK 애플리케이션 설정
translation-type: tm+mt
source-git-commit: b642bd1a136e62901847f2a8cf004d05282fca01
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 47%

---


# JavaScript 3.x 설정{#set-up-javascript}

## 전제 조건

* **올바른 구성 매개 변수 가져오기** 이러한 매개 변수는 Analytics 계정을 설정한 후 Adobe 담당자에게서 얻을 수 있습니다.
* **미디어 응용 프로그램`AppMeasurement`에서 JavaScript`Experience Cloud Identity Service`구현**&#x200B;및 [에 대한 자세한 내용은 JavaScript를 사용한](https://docs.adobe.com/content/help/ko-KR/analytics/implementation/js/overview.html) 분석 구현 [및 Experience Cloud Identity Service구현을 참조하십시오.](https://docs.adobe.com/content/help/en/id-service/using/implementation/setup-analytics.html)

* **미디어 플레이어에서 다음 기능 제공:**

   * *플레이어 이벤트에 가입할 API* - Media SDK를 사용하려면 이벤트가 플레이어에서 발생할 때 단순 API 세트를 호출해야 합니다.
   * *플레이어 정보를* 제공하는 API - 현재 재생 중인 미디어, 광고, 장에 대한 정보가 포함됩니다.

1. [다운로드한](/help/sdk-implement/download-sdks.md#download-3x-sdks) 라이브러리를 프로젝트에 추가합니다. 편의상 클래스에 대한 로컬 참조를 작성하십시오.

   1. 다운로드한 `MediaSDK-js-v3*.zip` 파일을 확장합니다.
   1. 다음 `MediaSDK.js` 파일이 `libs` 디렉토리에 있는지 확인합니다.

   1. `MediaSDK.js` 파일을 호스팅합니다.

      이 코어 JavaScript 파일은 사이트의 모든 페이지에 액세스할 수 있는 웹 서버에 호스팅해야 합니다. 다음 단계를 위해 이 파일에 대한 경로가 필요합니다.

   1. 모든 사이트 페이지에서 `MediaSDK.js`를 참조합니다.

      다음 코드 행을 각 페이지의 `MediaSDK` 또는 `<head>` 태그에 추가하여 JavaScript용 `<body>`를 포함합니다. 예:

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. 라이브러리를 성공적으로 가져왔는지를 신속하게 확인하려면 Window 개체에서 내보내졌는지 `ADB.Media` 확인합니다.

      >[!NOTE]
      >
      >The JavaScript SDK is compliant with the AMD and CommonJS module specifications, and `MediaSDK.js` can also be used with compatible module loaders.

1. 인스턴스를 만들고 `AppMeasurement` 구성합니다 `visitor`.

   미디어 SDK 구성에는 구성된 인스턴스 `AppMeasurement` 가 `visitor` 필요합니다.

   ```js
    var appMeasurement = new AppMeasurement(“<rsid>”);
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = “<visitor_namespace>.sc.omtrdc.net”;
   ```

1. 미디어 SDK 구성

   미디어 SDK는 웹 페이지당 한 번 구성되어야 하며 구성은 생성된 모든 추적기 인스턴스에 적용됩니다.

   >[!IMPORTANT]
   >
   > 미디어 SDK(3.x)는 2.x SDK에서 사용되는 HB 종단점과 다른 미디어 추적을 위해 미디어 컬렉션 API를 사용합니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.

   다음은 샘플 `MediaConfig` 초기화입니다.

   ```js
    // Create MediaConfig object (same as above)
    var mediaConfig = new ADB.MediaConfig();
    mediaConfig.trackingServer = Configuration.MEDIA_COLLECTION_ENDPOINT;
    mediaConfig.playerName = Configuration.PLAYER_NAME;
    mediaConfig.channel = Configuration.CHANNEL;
    mediaConfig.appVersion = Configuration.APP_VERSION;
    mediaConfig.debugLogging = false;
    mediaConfig.ssl = true;
   
    ADB.Media.configure(mediaConfig, appMeasurement);
   ```

1. `MediaTracker` 인스턴스를 생성합니다.

   미디어 SDK를 구성한 후 미디어 컨텐츠를 추적하기 위한 추적기 인스턴스를 `getInstance` API를 사용하여 만들 수 있습니다.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >미디어 세션이 끝날 때까지 이 인스턴스에 대한 할당이 취소되지 않는지 그리고 `tracker` 인스턴스가 액세스할 수 있는지 확인하십시오. 이 인스턴스는 해당 세션에 대해 다음 이벤트를 모두 추적하는 데 사용됩니다.

## JavaScript 2.x에서 3.x로 마이그레이션

2.x에서 3.x로 마이그레이션에 대한 자세한 정보는 [ 2.x에서 3.x로 마이그레이션](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)을 참조하십시오.
