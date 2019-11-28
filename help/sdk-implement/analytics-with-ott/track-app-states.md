---
title: 앱 상태 추적
description: '앱 상태는 애플리케이션의 다른 화면이나 보기이며, 표시되는 경우 trackState가 호출됩니다. '
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 앱 상태 추적{#track-app-states}

상태는 애플리케이션의 다양한 화면 또는 보기입니다. 애플리케이션에 새로운 상태가 표시될 때마다 `trackState` 호출을 전송해야 합니다. 예를 들어 사용자가 홈 페이지에서 비디오 세부 사항 화면으로 이동하면 `trackState` 호출을 보냅니다. 상태는 일반적으로 경로 지정 보고서를 사용하여 표시되므로 사용자가 앱을 이동하는 방법과 가장 많이 본 상태를 확인할 수 있습니다.

## trackState 호출

일반적으로 앱이 새 화면을 로드할 때마다 `trackState`를 호출합니다.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

상태 이름은 Adobe Mobile Services의 "보기 상태" 변수에 보고되며, 보기가 `trackState` 호출 별로 기록됩니다. 다른 Analytics 인터페이스에서 "보기 상태"는 "페이지 이름"으로 보고되며, "상태 보기"는 "페이지 보기"로 보고됩니다.

## 컨텍스트 데이터 보내기

상태 이름 외에도 각 추적 상태 호출로 추가 컨텍스트 데이터를 보낼 수 있습니다.

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
>컨텍스트 데이터 값은 Adobe Mobile Services에서 사용자 지정 변수에 매핑되어야 합니다.

