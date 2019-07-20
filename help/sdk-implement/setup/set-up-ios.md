---
seo-title: iOS 설정
title: iOS 설정
uuid: a 1 c 6 be 79-a 6 dc -47 b 6-93 b 3-ac 7 b 42 f 1 f 3 eb
translation-type: tm+mt
source-git-commit: 63fb6332694675cd03843995f8f86ae45973d399

---


# iOS 설정{#set-up-ios}

## 전제 조건

* **미디어 SDK**
에 대한 올바른 구성 매개 변수 얻기 이 매개 변수는 Analytics 계정을 설정한 후 Adobe 담당자로부터 얻을 수 있습니다.
* **애플리케이션에서**
iOS 용 adbmobile 구현 Adobe Mobile SDK 설명서에 대한 자세한 내용은 Experience Cloud 솔루션용 [iOS SDK 4. x를 참조하십시오.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/)

   >[!IMPORTANT]
   >
   >Apple는 iOS 9 부터 ATS (App Transport Security) 라는 기능을 도입했습니다. 이 기능은 앱에서 산업 표준 프로토콜과 암호만 사용하는지 확인하여 네트워크 보안을 향상시키기 위한 것입니다. 이 기능은 기본적으로 활성화되어 있지만, ATS 작업에 대한 선택 사항을 제공하는 구성 옵션이 있습니다. For details on ATS, see [App Transport Security.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/app_transport_security.html)

* **미디어 플레이어에 다음 기능을 제공합니다.**

   * _플레이어 이벤트에 가입할 API_ - Media SDK를 사용하려면 이벤트가 플레이어에서 발생할 때 단순 API 세트를 호출해야 합니다.
   * _플레이어 정보를 제공하는 API_ - 이 정보에는 미디어 이름 및 플레이헤드 위치와 같은 세부 사항이 포함되어 있습니다.

## SDK 구현

1. [다운로드한](../../sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) Media SDK를 프로젝트에 추가합니다.

   1. 다음 소프트웨어 구성 요소가 `libs` 디렉토리에 있는지 확인합니다.

      * `ADBMediaHeartbeat.h`: iOS 하트비트 추적 API에 사용되는 Objective-C 헤더 파일입니다.
      * `ADBMediaHeartbeatConfig.h`: SDK 구성에 대한 Objective-C 헤더 파일입니다.
      * `MediaSDK.a`: iOS 장치(armv7, armv7s, arm64)와 시뮬레이터(i386 and x86_64)의 라이브러리 빌드가 포함된 비트코드 사용 패트 바이너리입니다.

         iOS 앱이 타겟인 경우 이 바이너리를 연결해야 합니다.

      * `MediaSDK_TV.a`: 새 Apple TV 장치(arm64)와 시뮬레이터(x86_64)의 라이브러리 빌드가 포함된 비트코드 사용 패트 바이너리입니다.

         타겟이 Apple TV(tvOS) 앱용인 경우 이 바이너리를 연결해야 합니다.
   1. 라이브러리를 프로젝트에 추가합니다.

      1. Xcode IDE를 실행하고 앱을 엽니다.
      1. **[!UICONTROL Project Navigator]**&#x200B;에서 `libs` 디렉토리를 드래그하여 프로젝트 아래에 놓습니다.

      1. **[!UICONTROL 필요한 경우 항목 복사]** 확인란과 **[!UICONTROL 그룹 만들기]를 선택해야 하고**&#x200B;타겟에 추가&#x200B;**의 확인란은 아무것도 선택하면 안 됩니다.**

         ![](assets/choose-options_ios.png)

      1. **[!UICONTROL 마침을 클릭합니다]**.
      1. **[!UICONTROL 프로젝트 탐색기에서]**&#x200B;앱을 선택하고 타겟을 선택합니다.
      1. **[!UICONTROL 일반]** 탭의 **[!UICONTROL 연결된 프레임워크]** 및 **[!UICONTROL 라이브러리]** 섹션에서 필요한 프레임워크 및 라이브러리를 연결합니다.

         **iOS 앱 타겟:**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**
         **Apple TV(tvOS) 타겟:**

         * **AdobeMobileLibrary_TV.a**
         * **MediaSDK_TV.a**
         * **libsqlite3.0.tbd**
         * **SystemConfiguration.framework**
      1. 오류 없이 앱이 빌드되는지 확인합니다.




1. 라이브러리를 가져옵니다.

   ```
   #import "ADBMediaHeartbeat.h" 
   #import "ADBMediaHeartbeatConfig.h" 
   ```

1. `ADBMediaHeartbeatConfig` 인스턴스를 만듭니다.

   이 섹션은 `MediaHeartbeat` 구성 매개 변수를 이해하고, 정확한 추적을 위해 `MediaHeartbeat` 인스턴스에 올바른 구성 값을 설정하는 데 도움을 줍니다.

   다음은 샘플 `ADBMediaHeartbeatConfig` 초기화입니다.

   ```
   // Media Heartbeat Initialization 
   ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
   config.trackingServer = <SAMPLE_HEARTBEAT_TRACKING_SERVER>; 
   config.channel        = <SAMPLE_HEARTBEAT_CHANNEL>; 
   config.appVersion     = <SAMPLE_HEARTBEAT_SDK_VERSION>; 
   config.ovp            = <SAMPLE_HEARTBEAT_OVP_NAME>; 
   config.playerName     = <SAMPLE_PLAYER_NAME>; 
   config.ssl            = <YES/NO>; 
   config.debugLogging   = <YES/NO>; 
   ```

1. `ADBMediaHeartbeatDelegate` 프로토콜을 구현합니다.

   ```
   @interface VideoAnalyticsProvider : NSObject <ADBMediaHeartbeatDelegate> 
   
   @end 
   
   @implementation VideoAnalyticsProvider 
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames>  
   // with the current playback QoS values. 
   - (ADBMediaObject *)getQoSObject { 
       return [ADBMediaHeartbeat createQoSObjectWithBitrate:<bitrate>  
                                 startupTime:<startuptime>   
                                 fps:<fps>  
                                 droppedFrames:<droppedFrames>]; 
   } 
   
   // Return the current video player playhead position. 
   // Replace <currentPlaybackTime> with the video player current playback time 
   - (NSTimeInterval)getCurrentPlaybackTime { 
       return <currentPlaybackTime>; 
   } 
   
   @end
   ```

1. Use the `ADBMediaHeartBeatConfig` and `ADBMediaHeartBeatDelegate` to create the `ADBMediaHeartbeat` instance.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance 
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate: 
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >`ADBMediaHeartbeat` 인스턴스가 액세스 가능하고 세션이 끝날 *때까지*&#x200B;할당이 취소되지 않도록 해야 합니다. 이 인스턴스는 다음의 모든 추적 이벤트에 사용됩니다.

## iOS에서 버전 1.x에서 2.x로 마이그레이션 {#migrate-to-two-x}

버전 2.x에서 모든 공개 메서드는 개발자가 쉽게 만들 수 있도록 `ADBMediaHeartbeat` 클래스에 통합되어 있습니다. 모든 구성은 `ADBMediaHeartbeatConfig` 클래스에 통합되었습니다.

For more information about migrating from 1.x to 2.x, see [VHL 1.x to 2.x Migration.](../../sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## tvOS용 기본 앱 구성

새 Apple TV 릴리스에서 이제 기본 tvOS 환경에서 실행할 애플리케이션을 만들 수 있습니다. iOS에서 사용할 수 있는 여러 프레임워크를 사용하여 기본 앱을 생성하거나, XML 템플릿 및 JavaScript를 사용하여 앱을 만들 수 있습니다. MediaSDK 버전 2.0부터 tvOS에 대한 지원을 이용할 수 있습니다. For more information about tvOS, see [tvOS Developer site.](https://developer.apple.com/tvos/documentation/)

Xcode 프로젝트에서 다음 단계를 수행하십시오. 이 안내서는 tvOS를 타깃팅하는 Apple TV 앱 타겟이 프로젝트에 있다고 가정하여 작성되었습니다.

1. `VideoHeartbeat_TV.a` 라이브러리 파일을 프로젝트 `lib` 폴더로 드래그합니다.

1. tvOS 앱 대상의 **[!UICONTROL 빌드 단계]** 탭에서 **[!UICONTROL 라이브러리로 이진 링크]** 섹션을 확장하고 다음 라이브러리를 추가합니다.

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`

