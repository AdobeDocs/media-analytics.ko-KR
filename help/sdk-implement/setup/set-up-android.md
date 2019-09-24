---
seo-title: Android 설정
title: Android 설정
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Android 설정{#set-up-android}

## 전제 조건

* **Media SDK에 대한 유효한 구성 매개 변수**&#x200B;얻기 Adobe 담당자가 분석 계정을 설정한 후 이러한 매개 변수를 얻을 수 있습니다.
* **응용 프로그램에서** Android용 ADBMobile 구현Adobe Mobile SDK 설명서에 대한 자세한 내용은 Experience [Cloud 솔루션용 Android SDK 4.x를 참조하십시오.](https://marketing.adobe.com/resources/help/en_US/mobile/android/)
* **미디어 플레이어에 다음 기능을 제공합니다.**
   * *플레이어 이벤트에 가입할 API* - Media SDK를 사용하려면 이벤트가 플레이어에서 발생할 때 단순 API 세트를 호출해야 합니다.
   * *플레이어 정보를 제공하는 API* - 이 정보에는 미디어 이름 및 플레이헤드 위치와 같은 세부 사항이 포함되어 있습니다.

## SDK 구현

1. [다운로드한](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) Media SDK를 프로젝트에 추가합니다.

   1. Expand the Android zip file (e.g., `MediaSDK-android-v2.*.zip`).
   1. Verify that the `MediaSDK.jar` file exists in the `libs/` directory.

   1. 라이브러리를 프로젝트에 추가합니다.

      **IntelliJ IDEA:**

      1. **[!UICONTROL 프로젝트 탐색]** 패널에서 프로젝트를 마우스 오른쪽 버튼으로 클릭합니다.
      1. **[!UICONTROL 모듈 설정 열기를 선택합니다]**.
      1. Under **[!UICONTROL Project Settings]**, select **[!UICONTROL Libraries]**.

      1. Click **[!UICONTROL +]** to add a new library.
      1. **[!UICONTROL Java]**&#x200B;를 선택하고 `MediaSDK.jar` 파일로 이동합니다.

      1. 모바일 라이브러리를 사용할 모듈을 선택합니다.
      1. **[!UICONTROL 적용]**&#x200B;을 클릭한 다음 **[!UICONTROL 확인]**&#x200B;을 클릭하여 모듈 설정 창을 닫습니다.
      **Eclipse:**

      1. Eclipse IDE에서 프로젝트 이름을 마우스 오른쪽 버튼으로 클릭합니다.
      1. Click  **[!UICONTROL Build Path]** &gt; **[!UICONTROL Add External Archives]** .
      1. 선택 `MediaSDK.jar`.
      1. **[!UICONTROL 열기를 클릭합니다]**.
      1. Right-click the project again, and click  **[!UICONTROL Build Path]** &gt; **[!UICONTROL Configure Build Path]** .
      1. **[!UICONTROL 주문]** 및 **[!UICONTROL 내보내기]** 탭을 클릭합니다.

      1. `MediaSDK.jar` 파일을 선택했는지 확인합니다.


1. 라이브러리를 가져옵니다.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat; 
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate; 
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig; 
   import com.adobe.primetime.va.simple.MediaObject; 
   ```

1. Create the `MediaHeartbeatConfig` instance.

   다음은 샘플 `MediaHeartbeatConfig` 초기화입니다.

   ```java
   // Media Heartbeat Initialization 
   config.trackingServer = _<SAMPLE_HEARTBEAT_TRACKING_SERVER>_; 
   config.channel = <SAMPLE_HEARTBEAT_CHANNEL>; 
   config.appVersion = <SAMPLE_HEARTBEAT_SDK_VERSION>; 
   config.ovp =  <SAMPLE_HEARTBEAT_OVP_NAME>; 
   config.playerName = <SAMPLE_PLAYER_NAME>; 
   config.ssl = <true/false>; 
   config.debugLogging = <true/false>; 
   ```

1. Implement the `MediaHeartbeatDelegate` interface.

   ```java
   public class VideoAnalyticsProvider implements Observer, MediaHeartbeatDelegate{}
   ```

   ```java
   // Replace <bitrate>, <startupTime>, <fps>, and  
   // <droppeFrames> with the current playback QoS values.  
   @Override 
   public MediaObject getQoSObject() { 
       return MediaHeartbeat.createQoSObject(<bitrate>,  
                                             <startupTime>,  
                                             <fps>,  
                                             <droppedFrames>); 
   } 
   
   //Replace <currentPlaybackTime> with the video player current playback time 
   @Override 
   public Double getCurrentPlaybackTime() { 
       return <currentPlaybackTime>; 
   }
   ```

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` instance and the `MediaHertbeatDelegate` instance to create the `MediaHeartbeat` instance.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance 
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and *does not get deallocated until the end of the session*. 이 인스턴스는 다음의 모든 추적 이벤트에 사용됩니다.

**앱 권한 추가**

Media SDK를 사용하는 앱에서는 추적 호출에서 데이터를 전송하기 위해 다음 권한이 필요합니다.

* `INTERNET`
* `ACCESS_NETWORK_STATE`

이러한 권한을 추가하려면 애플리케이션 프로젝트 디렉토리의 `AndroidManifest.xml` 파일에 다음 줄을 추가합니다.

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Android에서 버전 1.x에서 2.x로 마이그레이션**

버전 2.x에서는 모든 공개 메서드가 개발자가 쉽게 만들 수 있도록 `com.adobe.primetime.va.simple.MediaHeartbeat` 클래스에 통합되어 있습니다. 또한 모든 구성이 이제 `com.adobe.primetime.va.simple.MediaHeartbeatConfig` 클래스에 통합되어 있습니다.

1.x에서 2.x로 마이그레이션에 대한 자세한 내용은 [mig-1x-2x-overview.md를 참조하십시오.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
