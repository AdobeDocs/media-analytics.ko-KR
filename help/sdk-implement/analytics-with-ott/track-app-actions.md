---
title: 앱 작업 추적
description: 앱 작업은 측정할 앱에서 발생하는 이벤트입니다.
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 앱 작업 추적{#track-app-actions}

작업은 측정할 앱에서 발생하는 이벤트입니다.

각 작업에는 이벤트가 발생할 때마다 늘어나는 하나 이상의 해당 지표가 있습니다. For example, you might send a `trackAction` call for each new subscription, or each time content is rated, or each time a level is completed.

작업이 자동으로 추적되지 않으므로 추적하려는 이벤트가 발생할 때 `trackAction`을 호출한 다음 사용자 지정 이벤트에 해당 작업을 매핑해야 합니다.

1. When an event that you want to track occurs, call `trackAction`.

   * **Roku:**

      ```js
      ADBMobile().trackAction("myapp.ActionName", {})
      ```

   * **Chromecast:**

      ```js
      ADBMobile.analytics.trackAction("myapp.ActionName", {});
      ```

1. 해당 작업을 사용자 지정 이벤트에 매핑합니다.

   * **Roku:**

      ```js
      dictionary = {} 
      dictionary["myapp.social.SocialSource"] = "Twitter"  
      ADBMobile().trackAction("myapp.SocialShare", dictionary)
      ```

   * **Chromecast:**

      ```js
      var dictionary = {}; 
      dictionary["myapp.social.SocialSource"] = "Twitter"; 
      ADBMobile.analytics.trackAction("myapp.SocialShare", dictionary);
      ```

각 트랙 작업 호출로 추가 컨텍스트 데이터를 전송할 수도 있습니다.

