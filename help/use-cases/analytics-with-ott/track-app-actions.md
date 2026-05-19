---
title: 앱 작업 추적
description: 앱 작업은 측정할 앱에서 발생하는 이벤트입니다.
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
exl-id: 88b7d540-67b7-4ec1-8273-02e34853bf60
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/ahqWp2yjs-zkd9dTRWTkE7b6KE-WpwVR0OH9vCqTPjI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 132
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
