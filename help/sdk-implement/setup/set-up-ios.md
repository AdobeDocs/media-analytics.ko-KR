---
title: iOS 설정
description: iOS에서 구현을 위한 Media SDK 애플리케이션 설정입니다.
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
translation-type: tm+mt
source-git-commit: f54733c44e96c517d0c4c624a40742b421a54325
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 99%

---


# iOS 설정{#set-up-ios}

>[!IMPORTANT]
>
>2021년 8월 31일에 버전 4 Mobile SDK에 대한 지원이 종료됨에 따라 Adobe는 iOS 및 Android용 Media Analytics SDK에 대한 지원도 종료할 예정입니다.  자세한 내용은 [Media Analytics SDK 지원 종료 FAQ](/help/sdk-implement/end-of-support-faqs.md)를 참조하십시오.

## 전제 조건

* **Media SDK에 대한 올바른 구성 매개 변수 가져오기**
이러한 매개 변수는 분석 계정을 설정한 후 Adobe 담당자에게서 얻을 수 있습니다.
* **애플리케이션에 iOS용 ADBMobile 구현**
Adobe Mobile SDK 설명서에 대한 자세한 내용은 [Experience Cloud 솔루션용 iOS SDK 4.x](https://docs.adobe.com/content/help/ko-KR/mobile-services/ios/overview.html)를 참조하십시오.

   >[!IMPORTANT]
   >
   >Apple은 iOS 9부터 ATS(앱 전송 보안)라는 기능을 도입했습니다. 이 기능은 앱에서 업계 표준 프로토콜과 암호만 사용하도록 함으로써 네트워크 보안을 개선하는 것을 목표로 합니다. 이 기능은 기본적으로 활성화되어 있지만 ATS 작업 옵션을 제공하는 구성 옵션이 있습니다. ATS에 대한 자세한 내용은 [앱 전송 보안](https://docs.adobe.com/content/help/ko-KR/mobile-services/ios/config-ios/app-transport-security.html)을 참조하십시오.

* **미디어 플레이어에서 다음 기능 제공:**

   * _플레이어 이벤트에 가입할 API_ - Media SDK를 사용하려면 이벤트가 플레이어에서 발생할 때 단순 API 세트를 호출해야 합니다.
   * _플레이어 정보를 제공하는 API_ - 이 정보에는 미디어 이름 및 재생 헤드 위치와 같은 세부 정보가 포함됩니다.

## SDK 구현

>[!IMPORTANT]
>
>버전 2.3.0부터 SDK는 XCFrameworks를 통해 배포됩니다.
>
>SDK 버전 2.3.0에는 Xcode 12.0 이상이 필요하며, 해당되는 경우 Cocoapods 1.10.0 이상이 필요합니다.

* 바이너리 라이브러리 파일이 언급될 때마다 대신 해당 XCFramework 대체 파일을 사용해야 합니다.
   * MediaSDK.a > MediaSDK.xcframework
   * MediaSDK_TV.a > MediaSDKTV.xcframework
* Adobe XCFrameworks를 프로젝트에 수동으로 추가하는 경우 XCFrameworks가 포함되지 않았는지 확인합니다.

1. [다운로드한](/help/sdk-implement/download-sdks.md#download-2x-sdks) Media SDK를 프로젝트에 추가합니다.

   1. 다음 소프트웨어 구성 요소가 `libs` 디렉토리에 있는지 확인합니다.

      * `ADBMediaHeartbeat.h`: iOS 하트비트 추적 API에 사용되는 Objective-C 헤더 파일입니다.
      * `ADBMediaHeartbeatConfig.h`: SDK 구성에 대한 Objective-C 헤더 파일입니다.
      * `MediaSDK.a`: iOS 장치(armv7, armv7s, arm64)와 시뮬레이터(i386 and x86_64)의 라이브러리 빌드가 포함된 비트코드 사용 패트 바이너리입니다.

         iOS 앱이 타겟인 경우 이 바이너리를 연결해야 합니다.

      * `MediaSDK_TV.a`: 새 Apple TV 장치(arm64)와 시뮬레이터(x86_64)의 라이브러리 빌드가 포함된 비트코드 사용 패트 바이너리입니다.

         Apple TV(tvOS) 앱이 타겟인 경우 이 바이너리를 연결해야 합니다.
   1. 라이브러리를 프로젝트에 추가합니다:

      1. Xcode IDE를 실행하고 앱을 엽니다.
      1. **[!UICONTROL 프로젝트 탐색기]**&#x200B;에서 `libs` 디렉토리를 드래그하여 프로젝트 아래에 놓습니다.

      1. **[!UICONTROL 필요한 경우 항목 복사]** 확인란과 **[!UICONTROL 그룹 만들기]**&#x200B;를 선택해야 하고 타겟에 추가&#x200B;**[!UICONTROL 의 확인란은 아무것도 선택하면 안 됩니다.]**

         ![](assets/choose-options_ios.png)

      1. **[!UICONTROL 마침을 클릭합니다]**.
      1. 앱을 **[!UICONTROL 프로젝트 탐색기]**&#x200B;에서 선택하고 타겟을 선택합니다.
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

1. `ADBMediaHeartBeatConfig` 및 `ADBMediaHeartBeatDelegate`를 사용하여 `ADBMediaHeartbeat` 인스턴스를 생성합니다.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate:
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >`ADBMediaHeartbeat` 인스턴스가 액세스할 수 있는지 그리고 *세션이 끝날 때까지 이 인스턴스에 대한 할당이 취소되지 않는지* 확인하십시오. 이 인스턴스는 다음의 모든 추적 이벤트에 사용됩니다.

## iOS에서 버전 1.x에서 2.x로 마이그레이션 {#migrate-to-two-x}

버전 2.x에서 모든 공개 메서드는 개발자가 쉽게 만들 수 있도록 `ADBMediaHeartbeat` 클래스에 통합되어 있습니다. 모든 구성은 `ADBMediaHeartbeatConfig` 클래스에 통합되었습니다.

1.x에서 2.x로 마이그레이션에 대한 자세한 내용은 [VHL 1.x에서 2.x로 마이그레이션](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)을 참조하십시오.

## tvOS용 기본 앱 구성

이제 새로운 Apple TV 릴리스로 기본 tvOS 환경에서 실행할 애플리케이션을 만들 수 있습니다. iOS에서 사용 가능한 여러 프레임워크를 사용하여 완전히 기본적인 앱을 만들거나 XML 템플릿 및 JavaScript를 사용하여 앱을 만들 수 있습니다. MediaSDK 버전 2.0부터 tvOS에 대한 지원을 이용할 수 있습니다. tvOS에 대한 자세한 내용은 [tvOS 개발자 사이트](https://developer.apple.com/tvos/)를 참조하십시오.

Xcode 프로젝트에서 다음 단계를 수행하십시오. 이 안내서는 프로젝트에 tvOS를 타깃팅하는 Apple TV 앱이 있다고 가정하고 작성되었습니다.

1. 프로젝트의 `lib` 폴더로 `VideoHeartbeat_TV.a` 라이브러리 파일을 드래그합니다.

1. tvOS 앱 대상의 **[!UICONTROL 빌드 단계]** 탭에서 **[!UICONTROL 라이브러리로 이진 링크]** 섹션을 확장하고 다음 라이브러리를 추가합니다.

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`
