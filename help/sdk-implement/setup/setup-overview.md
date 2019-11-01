---
title: 설정 개요
description: 모바일, OTT 및 브라우저(JS) 애플리케이션에서 미디어 추적을 위한 미디어 SDK 설정에 대한 개요입니다.
uuid: 06feeddb-b0c8-4f7d-90c8-e374cdde1695
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 설정 개요{#setup-overview}

>[!IMPORTANT]
>
>다음 지침은 2.x Media SDK에 적용됩니다. Media SDK의 1.x 버전을 구현하는 경우 [1.x Media SDK 설명서를 참조하십시오.](/help/sdk-implement/download-sdks.md) Primetime 통합업체의 경우 _아래 Primetime 미디어 SDK 설명서를_ 참조하십시오.


## 최소 플랫폼 버전 지원 {#minimum-platform-version}

다음 표에서는 2019년 2월 19일부터 각 SDK에 대해 지원되는 최소 플랫폼 버전에 대해 설명합니다.

| OS/브라우저 | 최소 버전 필요 |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0+ - Lollipop |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## 일반 구현 지침 {#general-implementation-guidelines}

다음과 같이 미디어 추적에 관련된 세 가지 기본 SDK 구성 요소가 있습니다.
* 미디어 하트비트 구성 - 이 구성에 보고할 기본 설정이 포함되어 있습니다.
* 미디어 하트비트 위임 - 이 위임은 재생 시간 및 QoS 개체를 제어합니다.
* 미디어 하트비트 - 구성원 및 메서드가 포함된 기본 라이브러리입니다.

다음 구현 단계를 완료합니다.

1. Create a `MediaHeartbeatConfig` instance and set your config parameter values.

   |  변수 이름  | 설명  | 필수 여부 |  기본값  |
   |---|---|:---:|---|
   | `trackingServer` | Media Analytics를 위한 추적 서버입니다. 이 서버는 Analytics 추적 서버와 다릅니다. | 예 | 빈 문자열 |
   | `channel` | 채널 이름 | 아니오 | 빈 문자열 |
   | `ovp` | 컨텐츠가 배포되는 온라인 미디어 플랫폼의 이름입니다. | 아니오 | 빈 문자열 |
   | `appVersion` | 미디어 플레이어 앱/SDK의 버전입니다. | 아니오 | 빈 문자열 |
   | `playerName` | 사용 중인 미디어 플레이어의 이름입니다. 예: "AVPlayer", "HTML5 Player", "My Custom Player" | 아니오 | 빈 문자열 |
   | `ssl` | 호출이 HTTPS를 통해 수행돼야 하는지 여부를 나타냅니다. | 아니오 | false |
   | `debugLogging` | 디버그 로깅이 사용되는지 여부를 나타냅니다. | 아니오 | false |

1. Implement the `MediaHeartbeatDelegate`.

   |  메서드 이름  |  설명  | 필수 여부 |
   | --- | --- | :---: |
   | `getQoSObject()` | 현재 QoS 정보가 포함된 `MediaObject` 인스턴스를 반환합니다. 이 메서드는 재생 세션 중에 여러 번 호출됩니다. 플레이어 구현은 항상 최근에 사용 가능한 QoS 데이터를 반환해야 합니다. | 예 |
   | `getCurrentPlaybackTime()` | 플레이헤드의 현재 위치를 반환합니다. VOD 추적의 경우 이 값은 미디어 항목이 시작된 후 현재까지의 시간(초)으로 지정됩니다. LINEAR/LIVE 추적의 경우 이 값은 프로그램이 시작된 후 현재까지의 시간(초)으로 지정됩니다. | 예 |

   >[!TIP]
   >
   >QoS(서비스 품질) 개체는 선택 사항입니다. 플레이어에 대해 QoS 데이터를 사용할 수 있고 해당 데이터를 추적하려는 경우 다음 변수가 필요합니다.

   | 변수 이름 | 설명   | 필수 여부 |
   | --- | --- | :---: |
   | `bitrate` | 미디어의 비트율(초당 비트 수)입니다. | 예 |
   | `startupTime` | 미디어의 시작 시간(밀리초)입니다. | 예 |
   | `fps` | 초당 표시되는 프레임입니다. | 예 |
   | `droppedFrames` | 지금까지 드롭된 프레임 수. | 예 |

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHertbeatConfig` and `MediaHertbeatDelegate` to create the `MediaHeartbeat` instance.

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the session. 이 인스턴스는 다음의 모든 미디어 추적 이벤트에 사용됩니다.

   >[!TIP]
   >
   >`MediaHeartbeat` adobe Analytics에 호출을 `AppMeasurement` 전송하는 인스턴스가 필요합니다.

1. 모든 부분을 결합합니다.

   다음 샘플 코드는 HTML5 비디오 플레이어에 JavaScript 2.x SDK를 사용합니다.

   ```javascript
   // Create local references to the heartbeat classes 
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   
   //Media Heartbeat Config 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = "[your_namespace].hb.omtrdc.net"; 
   mediaConfig.playerName = "HTML5 Basic"; 
   mediaConfig.channel = "Video Channel"; 
   mediaConfig.debugLogging = true; 
   mediaConfig.appVersion = "2.0"; 
   mediaConfig.ssl = false; 
   mediaConfig.ovp = ""; 
   
   // Media Heartbeat Delegate 
   var mediaDelegate = new MediaHeartbeatDelegate(); 
   
   // Set mediaDelegate CurrentPlaybackTime 
   mediaDelegate.getCurrentPlaybackTime = function() { 
       return video.currentTime; 
   }; 
   
   // Set mediaDelegate QoSObject - OPTIONAL 
   mediaDelegate.getQoSObject = function() { 
       return MediaHeartbeat.createQoSObject(video.bitrate,  
                                             video.startuptime,  
                                             video.fps,  
                                             video.droppedframes); 
   } 
   // Create mediaHeartbeat instance      
   this.mediaHeartbeat =  
     new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurementInstance);  
   ```

## 유효성 검사 {#validate}

Media Analytics 추적 구현에서는 두 가지 유형의 추적 호출을 생성합니다.

* 미디어 및 광고 시작 호출은 Adobe Analytics(AppMeasurement) 서버로 직접 전송됩니다.
* 하트비트 호출은 Media Analytics(하트비트) 추적 서버로 전송되어 처리되고 Adobe Analytics 서버로 전달됩니다.

* **Adobe Analytics(AppMeasurement) 서버**&#x200B;추적 서버 옵션에 대한 자세한 내용은 trackingServer [및 trackingServerSecure 변수 올바로 채우기를 참조하십시오.](https://helpx.adobe.com/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >Experience Cloud 방문자 ID 서비스에 대해 RDC 추적 서버 또는 CNAME에서 RDC 서버로 확인이 필요합니다.

   The analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

* ** 미디어 분석(하트비트) 서버**항상 "`[your_namespace].hb.omtrdc.net`" 형식을 갖습니다. "`[your_namespace]`"의 값은 회사를 지정하며 Adobe에서 제공합니다.

미디어 추적은 모든 플랫폼, 데스크탑 및 모바일에서 동일하게 작동합니다. 현재 모바일 플랫폼에서 오디오 추적이 작동합니다. 모든 추적 호출에 대해 확인해야 하는 몇 가지 주요 범용 변수가 있습니다.

## SDK 1.x 설명서 {#sdk-1x-documentation}

| 비디오 분석 1.x SDK |  개발자 가이드(PDF만 해당) |
| --- | --- |
| Android | ](vhl-dev-guide-v15_android.pdf)Android에 대한 구성 [ |
| AppleTV | ](vhl-dev-guide-v1x_appletv.pdf)AppleTV에 대한 구성 [ |
| Chromecast | [Chromecast에 대한 구성 ](chromecast_1.x_sdk.pdf) |
| iOS | [iOS에 대한 구성 ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [JavaScript에 대한 구성 ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [TVML에 대한 구성 ](vhl_tvml.pdf) |

## Primetime Media SDK 설명서 {#primetime-docs}

* [Primetime 사용자 안내서](https://helpx.adobe.com/primetime/user-guide.html)
