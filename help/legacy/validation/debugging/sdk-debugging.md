---
title: SDK 디버깅
description: Media SDK에서 사용할 수 있는 추적/로깅에 대해 알아봅니다.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
exl-id: c2de6454-8538-4d07-a099-e278b153d894
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 100%

---

# SDK 디버깅{#sdk-debugging}

로그를 활성화하고 비활성화할 수 있습니다. Media SDK는 미디어 추적 스택 전체에서 광범위한 추적/로그 메커니즘을 제공합니다. 구성 개체에 `debugLogging` 플래그를 설정하여 로그를 활성화하거나 비활성화할 수 있습니다.

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

## 로그 메시지

로그 메시지는 다음 형식을 따릅니다.

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>]
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **timestamp:** 현재 CPU 시간(GMT 시간대)입니다.
* **level:** 4개의 메시지 수준이 정의되어 있습니다.
   * 정보 - 일반적으로 애플리케이션의 입력 데이터(플레이어 이름, 비디오 ID 등의 유효성을 검사합니다.)
   * 디버그 - 개발자가 더 복잡한 문제를 디버깅하는 데 사용하는 디버그 로그
   * 경고 - 잠재적인 통합/구성 오류나 하트비트 SDK 버그를 나타냅니다.
   * 오류 - 중요한 통합 오류나 하트비트 SDK 버그를 나타냅니다.
* **태그:** 로그 메시지를 발행한 하위 구성 요소의 이름(일반적으로 클래스 이름)
* **메시지:** 실제 추적 메시지

Media SDK 라이브러리의 로그 출력을 사용하여 구현을 확인할 수 있습니다. 유용한 전략은 로그에서 `#track` 문자열을 검색하는 것입니다. 이 경우 애플리케이션의 모든 `track*()` 호출이 강조 표시됩니다.

예를 들어 `#track`에 대해 필터링된 로그 모양은 다음과 같습니다.

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
