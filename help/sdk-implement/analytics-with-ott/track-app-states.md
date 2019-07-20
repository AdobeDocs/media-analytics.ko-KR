---
seo-title: 앱 상태 추적
title: 앱 상태 추적
uuid: 2 F 98 FB 43-C 362-4 A 9 B -8732-FA 7 E 963 DA 729
translation-type: tm+mt
source-git-commit: 9cdf69e30fa727aeb974213769a7ab61fb05b756

---


# 앱 상태 추적{#track-app-states}

상태는 애플리케이션의 다양한 화면 또는 보기입니다. Each time a new state is displayed in your application, you should send a `trackState` call. For example, when a user navigates from the home page to the video details screen, send a `trackState` call. 상태는 일반적으로 경로 지정 보고서를 사용하여 표시되므로 사용자가 앱을 이동하는 방법과 가장 많이 본 상태를 확인할 수 있습니다.

## trackState 호출

You typically call `trackState` each time the app loads a new screen.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. 다른 Analytics 인터페이스에서 "보기 상태" 는 "페이지 이름" 로 보고됩니다. " 상태 보기 "는" 페이지 보기 횟수 "로 보고됩니다.

## 컨텍스트 데이터 보내기

" 상태 이름 "외에도 각 추적 상태 호출을 사용하여 추가 컨텍스트 데이터를 보낼 수 있습니다.

### Roku

```js
dictionary = { } 
dictionary["myapp.login.LoginStatus"] = "logged in"  
ADBMobile().trackState("Home Screen", dictionary)
```

### Chromecast

```js
var dictionary = { }; 
dictionary["myapp.login.LoginStatus"] = "logged in"; 
ADBMobile.analytics.trackState("Home Screen", dictionary); 
```

>[!NOTE]
>
>컨텍스트 데이터 값은 Adobe Mobile Services에서 사용자 지정 변수로 매핑되어야 합니다.

