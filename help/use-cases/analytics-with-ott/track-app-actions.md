---
title: 앱 작업 추적
description: 앱 작업은 측정할 앱에서 발생하는 이벤트입니다.
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
exl-id: 88b7d540-67b7-4ec1-8273-02e34853bf60
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 100%

---

# 앱 작업 추적{#track-app-actions}

작업은 측정할 앱에서 발생하는 이벤트입니다.

각 작업에는 이벤트가 발생할 때마다 늘어나는 하나 이상의 해당 지표가 있습니다. 예를 들어 콘텐츠에 등급이 매겨질 때마다 또는 수준이 완료될 때마다 각각의 새 가입에 대한 `trackAction` 호출을 보낼 수 있습니다.

작업이 자동으로 추적되지 않으므로 추적하려는 이벤트가 발생할 때 `trackAction`을 호출한 다음 사용자 지정 이벤트에 해당 작업을 매핑해야 합니다.

1. 추적할 이벤트가 발생하면 `trackAction`을 호출합니다.

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
