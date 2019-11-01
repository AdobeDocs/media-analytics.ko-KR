---
title: SDK 디버깅
description: 이 항목에서는 Media SDK에서 사용할 수 있는 추적/로깅에 대해 설명합니다.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# SDK 디버깅{#sdk-debugging}

로깅을 활성화하거나 비활성화할 수 있습니다. 미디어 SDK는 미디어 추적 스택 전체에서 광범위한 추적/로깅 메커니즘을 제공합니다. You can enable or disable logging by setting the `debugLogging` flag on the Config object.

## 디버그 로깅에 대한 샘플 코드

### Android

```java
// Media Heartbeat initialization 
MediaHeartbeatConfig config = new MediaHeartbeatConfig(); 
config.debugLogging = true; 

// Use this space for setting other config values 
MediaHeartbeat _heartbeat = new MediaHeartbeat(this, config); 
```

### iOS

```
// Media Heartbeat Initialization 
ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
config.debugLogging = YES; 

// Use this space for setting other config values 
ADBMediaHeartbeat *_mediaHeartbeat =  
[[ADBMediaHeartbeat alloc] initWithDelegate:self config:config]; 
```

### JavaScript

```js
// Media Heartbeat initialization 
var mediaConfig = new MediaHeartbeatConfig(); 
mediaConfig.debugLogging = true; 
this._mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement); 
```

### OTT(Chromecast, Roku)

ADBMobile 라이브러리는 `setDebugLogging` 메서드를 통해 디버그 로깅을 제공합니다. 모든 프로덕션 앱에 대해 디버그 로깅을 `false`로 설정해야 합니다.

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

## Adobe Bloodhound를 사용하여 Chromecast 애플리케이션 테스트

애플리케이션을 개발할 때 Bloodhound를 사용하면 로컬로 서버 호출을 볼 수 있으며 선택적으로 Adobe 수집 서버에 데이터를 전송할 수 있습니다. Bloodhound에 대한 자세한 내용은 다음 안내서를 참조하십시오.

* [Mac용 Bloodhound 3.x](https://marketing.adobe.com/resources/help/en_US/mobile/bloodhound/)
* [Bloodhound 2.2 for Windows](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)

>[!IMPORTANT]
>
>2017년 4월 30일 현재 Adobe Bloodhound는 종료되었습니다. 2017년 5월 1일부터 추가적인 개선이나 추가 엔지니어링 또는 Adobe Expert Care 지원이 제공되지 않습니다.

## 로그 메시지

로그 메시지는 다음 형식을 따릅니다.

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>] 
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **timestamp**: 현재 CPU 시간(GMT에 대한 시간대)
* **level**: 다음 4개의 메시지 수준이 정의되어 있습니다.
   * INFO – 일반적으로 애플리케이션의 입력 데이터임(플레이어 이름, 비디오 ID 등 확인)
   * DEBUG – 개발자가 훨씬 복잡한 문제를 디버그하는 데 사용하는 디버그 로그
   * WARN – 잠재적인 통합/구성 오류 또는 하트비트 SDK 버그를 나타냄
   * ERROR – 중요한 통합 오류 또는 하트비트 SDK 버그를 나타냄
* **tag**: 로그 메시지를 표시한 하위 구성 요소의 이름(일반적으로 클래스 이름)
* **message**: 실제 추적 메시지

Media SDK 라이브러리의 출력 로그를 사용하여 구현을 확인할 수 있습니다. A good strategy is to search through the logs for the string `#track`. This will highlight all the `track*()` calls made by your application.

For instance, this is what the logs filtered for `#track` could look like:

```js
[16:10:29 GMT­0700 (PDT).222] [INFO] [plugin::player] #trackVideoLoad() 
[16:10:29 GMT­0700 (PDT).230] [INFO] [plugin::player] #trackSessionStart() 
[16:10:29 GMT­0700 (PDT).250] [INFO] [plugin::player] #trackPlay() 
[16:10:29 GMT­0700 (PDT).759] [INFO] [plugin::player] #trackChapterStart() 
[16:10:44 GMT­0700 (PDT).769] [INFO] [plugin::player] #trackAdStart() 
[16:10:59 GMT­0700 (PDT).752] [INFO] [plugin::player] #trackAdComplete() 
[16:10:59 GMT­0700 (PDT).770] [INFO] [plugin::player] #trackChapterStart() 
[16:11:29 GMT­0700 (PDT).734] [INFO] [plugin::player] #trackPause() 
[16:11:29 GMT­0700 (PDT).764] [INFO] [plugin::player] #trackComplete() 
[16:11:29 GMT­0700 (PDT).766] [INFO] [plugin::player] #trackVideoUnload()
```

