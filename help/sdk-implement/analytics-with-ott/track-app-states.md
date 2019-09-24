---
seo-title: 앱 상태 추적
title: 앱 상태 추적
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
translation-type: tm+mt
source-git-commit: 9cdf69e30fa727aeb974213769a7ab61fb05b756

---


# 앱 상태 추적{#track-app-states}

상태는 애플리케이션의 다양한 화면 또는 보기입니다. Each time a new state is displayed in your application, you should send a  call. `trackState` For example, when a user navigates from the home page to the video details screen, send a  call. `trackState` 상태는 일반적으로 경로 지정 보고서를 사용하여 표시되므로 사용자가 앱을 이동하는 방법과 가장 많이 본 상태를 확인할 수 있습니다.

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

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. In other Analytics interfaces, "View State" is reported as "Page Name"; "State Views" is reported as "Page Views".

## Send context data

"상태 이름" 외에 각 추적 상태 호출을 사용하여 추가 컨텍스트 데이터를 전송할 수 있습니다.

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
>Context data values must be mapped to custom variables in Adobe Mobile services.

