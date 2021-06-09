---
title: Android 설정
description: Android에서 구현을 위한 Media SDK 애플리케이션 설정입니다.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
exl-id: 261445bf-3c8b-4658-891d-9a878e0b26ea
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 98%

---

# Android 설정{#set-up-android}

>[!IMPORTANT]
>
>2021년 8월 31일에 버전 4 Mobile SDK에 대한 지원이 종료됨에 따라 Adobe는 iOS 및 Android용 Media Analytics SDK에 대한 지원도 종료할 예정입니다.  자세한 내용은 [Media Analytics SDK 지원 종료 FAQ](/help/sdk-implement/end-of-support-faqs.md)를 참조하십시오.


## 전제 조건

* **Media SDK에 대한 올바른 구성 매개 변수 가져오기**
이러한 매개 변수는 분석 계정을 설정한 후 Adobe 담당자에게서 얻을 수 있습니다.
* **애플리케이션에 Android용 ADBMobile 구현** Adobe Mobile SDK 설명서에 대한 자세한 내용은 [Experience Cloud 솔루션용 Android SDK 4.x](https://experienceleague.adobe.com/docs/mobile-services/android/overview.html)를 참조하십시오.

* **미디어 플레이어에서 다음 기능 제공:**
   * *플레이어 이벤트에 가입할 API* - Media SDK를 사용하려면 이벤트가 플레이어에서 발생할 때 단순 API 세트를 호출해야 합니다.
   * *플레이어 정보를 제공하는 API* - 이 정보에는 미디어 이름 및 재생 헤드 위치와 같은 세부 정보가 포함됩니다.

## SDK 구현

1. [다운로드한](/help/sdk-implement/download-sdks.md#download-2x-sdks) Media SDK를 프로젝트에 추가합니다.

   1. Android zip 파일(예: `MediaSDK-android-v2.*.zip`)을 확장합니다.
   1. 다음 `MediaSDK.jar` 파일이 `libs/` 디렉토리에 있는지 확인합니다.

   1. 라이브러리를 프로젝트에 추가합니다.

      **IntelliJ IDEA:**

      1. **[!UICONTROL 프로젝트 탐색]** 패널에서 프로젝트를 마우스 오른쪽 버튼으로 클릭합니다.
      1. **[!UICONTROL 모듈 설정 열기]**&#x200B;를 선택합니다.
      1. **[!UICONTROL 프로젝트 설정]**&#x200B;에서 **[!UICONTROL 라이브러리]**&#x200B;를 선택합니다.

      1. 새 라이브러리를 **[!UICONTROL +]**&#x200B;를 클릭하여 추가합니다.
      1. **[!UICONTROL Java]**&#x200B;를 선택하고 `MediaSDK.jar` 파일로 이동합니다.

      1. 모바일 라이브러리를 사용할 모듈을 선택합니다.
      1. **[!UICONTROL 적용]**&#x200B;을 클릭한 다음 **[!UICONTROL 확인]**&#x200B;을 클릭하여 모듈 설정 창을 닫습니다.

      **Eclipse:**

      1. Eclipse IDE에서 프로젝트 이름을 마우스 오른쪽 버튼으로 클릭합니다.
      1. **[!UICONTROL 빌드 경로]** > **[!UICONTROL 외부 아카이브 추가]**&#x200B;를 클릭합니다.
      1. `MediaSDK.jar`을 선택합니다.
      1. **[!UICONTROL 열기]**&#x200B;를 클릭합니다.
      1. 프로젝트를 다시 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL 빌드 경로]** > **[!UICONTROL 빌드 경로 구성]**&#x200B;을 클릭합니다.
      1. **[!UICONTROL 주문]** 및 **[!UICONTROL 내보내기]** 탭을 클릭합니다.

      1. `MediaSDK.jar` 파일을 선택했는지 확인합니다.


1. 라이브러리를 가져옵니다.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat;
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate;
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig;
   import com.adobe.primetime.va.simple.MediaObject;
   ```

1. `MediaHeartbeatConfig` 인스턴스를 생성합니다.

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

1. `MediaHeartbeatDelegate` 인터페이스를 구현합니다.

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

1. `MediaHeartbeat` 인스턴스를 생성합니다.

   `MediaHeartbeatConfig` 인스턴스 및 `MediaHertbeatDelegate` 인스턴스를 사용하여 `MediaHeartbeat` 인스턴스를 만듭니다.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >`MediaHeartbeat` 인스턴스가 액세스할 수 있는지 그리고 *세션이 끝날 때까지 이 인스턴스에 대한 할당이 취소되지 않는지* 확인하십시오. 이 인스턴스는 다음의 모든 추적 이벤트에 사용됩니다.

**앱 권한 추가**

Media SDK를 사용하는 앱에서는 추적 호출에서 데이터를 전송하기 위해 다음 권한이 필요합니다.

* `INTERNET`
* `ACCESS_NETWORK_STATE`

이러한 권한을 추가하려면 애플리케이션 프로젝트 디렉토리의 `AndroidManifest.xml` 파일에 다음 줄을 추가합니다.

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Android에서 버전 1.x에서 2.x로 마이그레이션**

버전 2.x에서는 모든 공개 메서드가 개발자가 쉽게 만들 수 있도록 `com.adobe.primetime.va.simple.MediaHeartbeat` 클래스에 통합되어 있습니다. 또한 모든 구성이 이제 `com.adobe.primetime.va.simple.MediaHeartbeatConfig` 클래스에 통합되어 있습니다.

1.x에서 2.x로 마이그레이션에 대한 자세한 내용은 [mig-1x-2x-overview.md](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)를 참조하십시오.
