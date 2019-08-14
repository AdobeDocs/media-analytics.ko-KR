---
seo-title: 설정 개요
title: 설정 개요
uuid: 06 fefedb-b 0 c 8-4 f 7 d -90 c 8-e 374 cdde 1695
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# 설정 개요{#setup-overview}

>[!IMPORTANT]
>
>다음 지침은 2. x 미디어 SDK에 적용됩니다. Media SDK의 1.x 버전을 구현하는 경우 [1.x Media SDK 설명서를 참조하십시오.](/help/sdk-implement/download-sdks.md) Primetime 통합업체의 경우 아래의 _Primetime Media SDK 설명서를_ 참조하십시오.


## 최소 플랫폼 버전 지원 {#minimum-platform-version}

다음 표는 2019 년 2 월 19 일부터 각 SDK에 대해 지원되는 최소 플랫폼 버전에 대해 설명합니다.

| OS/Browser | 최소 버전 필요 |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0 + - Lollipop |
| Chrome | v 22 + |
| Mozilla | v 27 + |
| Safari | v 7 + |
| IE | v 11 + |

## 일반 구현 지침 {#section_965A3B699A8248DDB9B2B3EA3CC20E41}

다음과 같이 미디어 추적에 관련된 세 가지 기본 SDK 구성 요소가 있습니다.
* 미디어 하트비트 구성 - 이 구성에 보고할 기본 설정이 포함되어 있습니다.
* 미디어 하트비트 위임 - 이 위임은 재생 시간 및 QoS 개체를 제어합니다.
* 미디어 하트비트 - 구성원 및 메서드가 포함된 기본 라이브러리입니다.

다음 구현 단계를 완료합니다.

1. `MediaHeartbeatConfig` 인스턴스를 만들고 구성 매개 변수 값을 설정합니다.

   |  변수 이름  | 설명  | 필수 여부 |  기본값  |
   |---|---|:---:|---|
   | `trackingServer` | Media Analytics를 위한 추적 서버입니다. 이 서버는 Analytics 추적 서버와 다릅니다. | 예 | 빈 문자열 |
   | `channel` | 채널 이름 | 아니오 | 빈 문자열 |
   | `ovp` | 컨텐츠가 배포되는 온라인 미디어 플랫폼의 이름입니다. | 아니오 | 빈 문자열 |
   | `appVersion` | 미디어 플레이어 앱/SDK의 버전입니다. | 아니오 | 빈 문자열 |
   | `playerName` | 사용 중인 미디어 플레이어의 이름입니다. 예: "AVPlayer", "HTML5 Player", "My Custom Player" | 아니오 | 빈 문자열 |
   | `ssl` | 호출이 HTTPS를 통해 수행돼야 하는지 여부를 나타냅니다. | 아니오 | false |
   | `debugLogging` | 디버그 로깅이 사용되는지 여부를 나타냅니다. | 아니오 | false |

1. 을 구현합니다 `MediaHeartbeatDelegate`.

   |  메서드 이름  |  설명  | 필수 여부 |
   | --- | --- | :---: |
   | `getQoSObject()` | 현재 QoS 정보가 포함된 `MediaObject` 인스턴스를 반환합니다. 이 메서드는 재생 세션 중에 여러 번 호출됩니다. 플레이어 구현은 항상 최근에 사용 가능한 QoS 데이터를 반환해야 합니다. | 예 |
   | `getCurrentPlaybackTime()` | 플레이헤드의 현재 위치를 반환합니다. VOD 추적의 경우 이 값은 미디어 항목이 시작된 후 현재까지의 시간(초)으로 지정됩니다. LINEAR/LIVE 추적의 경우 이 값은 프로그램이 시작된 후 현재까지의 시간(초)으로 지정됩니다. | 예 |

   >[!TIP]
   >
   >Qos (서비스 품질) 개체는 선택 사항입니다. 플레이어에 대해 QoS 데이터를 사용할 수 있고 해당 데이터를 추적하려는 경우 다음 변수가 필요합니다.

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
   >`MediaHeartbeat` 인스턴스가 액세스 가능하고 세션이 끝날 때까지 할당이 취소되지 않도록 해야 합니다. 이 인스턴스는 다음의 모든 미디어 추적 이벤트에 사용됩니다.

   >[!TIP]
   >
   >`MediaHeartbeat` Adobe Analytics에 대한 호출을 `AppMeasurement` 보내려면의 인스턴스가 필요합니다.

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

## 유효성 검사 {#section_D4D46F537A4E442B8AB0BB979DDAA4CC}

미디어 구현은 다음과 같은 두 가지 유형의 추적 호출로 구성됩니다.

* 미디어 및 광고 시작 호출은 AppMeasurement 서버에 직접 전송됩니다.
* 하트 비트 호출은 시작 시, 컨텐츠에 대해서는 10초마다, 광고에 대해서는 1초마다 하트비트 추적 서버로 전송됩니다.

미디어 추적은 모든 플랫폼, 데스크탑 및 모바일에서 동일하게 작동합니다. 오디오 추적은 현재 모바일 플랫폼에서 작동합니다. 모든 추적 호출에 대해 확인해야 하는 몇 가지 주요 범용 변수가 있습니다.

* **Appmeasurement (Analytics)**
추적 서버 옵션에 대한 자세한 내용은 [Trackingserver 및 trackingserversecure 변수 올바로 채우기를 참조하십시오.](https://marketing.adobe.com/resources/help/kb/en_US/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >Experience Cloud 방문자 ID 서비스를 사용하려면 RDC 추적 서버 또는 RDC 서버로 CNAME 이 해결되어야 합니다.

   The analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

* ** 미디어 분석 (하트 비트)**
이 형식은 항상 형식을 갖습니다`[your_namespace].hb.omtrdc.net`. " 의 값은 회사를`[your_namespace]`지정하며 Adobe에서 제공합니다.

## SDK 1. x 설명서 {#section_acj_tkk_t2b}

| Video Analytics 1. x SDK  | 개발자 안내서 (PDF만 해당) |
| --- | --- |
| Android | ](vhl-dev-guide-v15_android.pdf)Android에 대한 구성 [ |
| AppleTV | ](vhl-dev-guide-v1x_appletv.pdf)AppleTV에 대한 구성 [ |
| Chromecast | [Chromecast에 대한 구성 ](chromecast_1.x_sdk.pdf) |
| iOS | [iOS에 대한 구성 ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [JavaScript에 대한 구성 ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [TVML에 대한 구성 ](vhl_tvml.pdf) |

## Primetime Media SDK 설명서 {#primetime-docs}

* [Primetime 사용 안내서](https://helpx.adobe.com/primetime/user-guide.html)
