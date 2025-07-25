---
title: 레거시 Media SDK 구현 설명
description: “모바일, OTT 및 브라우저(JS) 애플리케이션에서 미디어 추적을 위해 **레거시** 2.x Media SDK를 설정하는 방법을 알아봅니다.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: d94ede3e-95f8-4591-9833-ef39aff12ba9
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 99%

---

# 레거시 2.x Streaming Media SDK 설정 개요{#setup-overview}

이 섹션의 지침은 **레거시** 2.x Media SDK에 적용됩니다.

* Media SDK의 1.x 버전의 구현에 대한 내용은 [1.x Media SDK 설명서를 참조하십시오.](/help/getting-started/download-sdks.md)

* Primetime 통합 업체의 경우, _Primetime Media SDK 설명서_&#x200B;를 참조하십시오.

>[!IMPORTANT]
>
>2021년 8월 31일에 버전 4 Mobile SDK에 대한 지원이 종료됨에 따라 Adobe는 iOS 및 Android용 Media Analytics SDK에 대한 지원도 종료할 예정입니다.  자세한 내용은 [Media Analytics SDK 지원 종료 FAQ](/help/additional-resources/end-of-support-faqs.md)를 참조하십시오.


## 최소 플랫폼 버전 지원 {#minimum-platform-version}

다음 테이블에서는 2019년 2월 19일부터 각 SDK에 대해 지원되는 최소 플랫폼 버전에 대해 설명합니다.

| OS/브라우저 | 필요한 최소 버전 |
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

1. 매개 변수 값을 설정하고 `MediaHeartbeatConfig` 인스턴스를 작성합니다.

   |  변수 이름  | 설명  | 필수 여부 |  기본값  |
   |---|---|:---:|---|
   | `trackingServer` | 미디어 분석을 위한 추적 서버입니다. 분석 추적 서버와 다릅니다. | 예 | 빈 문자열 |
   | `channel` | 채널 이름 | 아니요 | 빈 문자열 |
   | `ovp` | 콘텐츠가 배포되는 온라인 미디어 플랫폼의 이름입니다. | 아니요 | 빈 문자열 |
   | `appVersion` | 미디어 플레이어 앱/SDK의 버전입니다. | 아니요 | 빈 문자열 |
   | `playerName` | 사용 중인 미디어 플레이어의 이름입니다. 예: &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom Player&quot; | 아니요 | 빈 문자열 |
   | `ssl` | 호출이 HTTPS를 통해 수행되야 하는지 여부를 나타냅니다. | 아니요 | false |
   | `debugLogging` | 디버그 로깅이 사용되는지 여부를 나타냅니다. | 아니요 | false |

1. `MediaHeartbeatDelegate`를 구현합니다.

   |  메서드 이름  |  설명  | 필수 여부 |
   | --- | --- | :---: |
   | `getQoSObject()` | 현재 QoS 정보가 포함된 `MediaObject` 인스턴스를 반환합니다. 이 메서드는 재생 세션 중에 여러 번 호출됩니다. 플레이어 구현은 항상 최근에 사용 가능한 QoS 데이터를 반환해야 합니다. | 예 |
   | `getCurrentPlaybackTime()` | 플레이헤드의 현재 위치를 반환합니다. <br /> VOD 추적의 경우 이 값은 미디어 항목이 시작된 후 현재까지의 시간(초)으로 지정됩니다. <br /> 라이브 스트리밍의 경우 플레이어가 콘텐츠 지속 시간에 대한 정보를 제공하지 않으면 해당 날짜의 자정(UTC) 이후 경과된 시간(초 수)으로 값을 지정할 수 있습니다. <br /> 참고: 진행률 마커를 사용할 경우 콘텐츠 지속 시간이 필요하며 플레이헤드는 0부터 시작하여 미디어 항목의 시작부터 초 단위로 업데이트해야 합니다. | 예 |

   >[!TIP]
   >
   >QoS(서비스 품질) 개체는 선택 사항입니다. 플레이어에 대해 QoS 데이터를 사용할 수 있고 해당 데이터를 추적하려는 경우 다음 변수가 필요합니다.

   | 변수 이름 | 설명   | 필수 여부 |
   | --- | --- | :---: |
   | `bitrate` | 초당 비트 수 단위의 미디어 비트율. | 예 |
   | `startupTime` | 밀리초 단위의 미디어 시작 시간. | 예 |
   | `fps` | 초당 표시되는 프레임 수. | 예 |
   | `droppedFrames` | 지금까지 드롭된 프레임 수. | 예 |

1. `MediaHeartbeat` 인스턴스를 생성합니다.

   `MediaHertbeatConfig` 및 `MediaHertbeatDelegate`를 사용하여 `MediaHeartbeat` 인스턴스를 생성합니다.

   >[!IMPORTANT]
   >
   >세션이 끝날 때까지 이 인스턴스에 대한 할당이 취소되지 않는지 그리고 `MediaHeartbeat` 인스턴스가 액세스할 수 있는지 확인하십시오. 이 인스턴스는 다음의 모든 미디어 추적 이벤트에 사용됩니다.

   >[!TIP]
   >
   >Adobe Analytics에 대한 호출을 전송하려면 `MediaHeartbeat`에 `AppMeasurement`의 인스턴스가 필요합니다.

1. 모든 조각을 결합합니다.

   다음 샘플 코드는 HTML5 비디오 플레이어에 Adobe의 JavaScript 2.x SDK를 사용합니다.

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

Media Analytics 추적 구현에서는 다음 두 가지 유형의 추적 호출을 생성합니다.

* 미디어 및 광고 시작 호출은 Adobe Analytics(AppMeasurement) 서버에 직접 전송됩니다.
* 하트비트 호출은 Media Analytics(하트비트) 추적 서버로 전송되어 처리되고, Adobe Analytics 서버로 전달됩니다.

* **Adobe Analytics(AppMeasurement) 서버**
추적 서버 옵션에 대한 자세한 내용은 [trackingServer 및 trackingServerSecure 변수를 올바르게 채우기](https://helpx.adobe.com/kr/analytics/kb/determining-data-center.html)를 참조하십시오.

  >[!IMPORTANT]
  >
  >RDC 서버로 확인되는 RDC 추적 서버 또는 CNAME은 Experience Cloud 방문자 ID 서비스에 필요합니다.

  Analytics 추적 서버는 &quot;`.sc.omtrdc.net`&quot;으로 끝나야 하거나 CNAME이어야 합니다.

* **&#x200B; Media Analytics(하트비트) 서버**
항상 &quot;`[your_namespace].hb.omtrdc.net`&quot; 형식입니다. 다음 &quot;`[your_namespace]`&quot;의 값은 회사를 지정하며, Adobe에서 제공합니다.

미디어 추적은 모든 플랫폼, 데스크탑 및 모바일에서 동일하게 작동합니다. 오디오 추적은 현재 모바일 플랫폼에서 작동합니다. 모든 추적 호출에 대해 확인해야 하는 몇 가지 주요 범용 변수가 있습니다.

## SDK 1.x 설명서 {#sdk-1x-documentation}

| Video Analytics 1.x SDKs  |  개발자 안내서(PDF만 해당) |
| --- | --- |
| Android | [&#128279;](vhl-dev-guide-v15_android.pdf)Android에 대한 구성 |
| Apple TV | [Apple TV에 대한 구성](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Chromecast에 대한 구성](chromecast_1.x_sdk.pdf) |
| iOS | [iOS에 대한 구성](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [JavaScript에 대한 구성](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android:   [Media Analytics 구성](https://help.adobe.com/ko_KR/primetime/psdk/android/1.4/index.html) </li> <li> DHLS:   [Media Analytics 구성](https://help.adobe.com/ko_KR/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS:   [Media Analytics 구성](https://help.adobe.com/ko_KR/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [TVML에 대한 구성](vhl_tvml.pdf) |

## Primetime Media SDK 설명서 {#primetime-docs}

* [Primetime 사용 안내서](https://helpx.adobe.com/primetime/user-guide.html)
