---
title: Chromecast에서 코어 재생 추적
description: 이 항목에서는 Chromecast에서 Media SDK를 사용하여 핵심 추적을 구현하는 방법에 대해 설명합니다.
uuid: a9fc59d8-a2f4-4889-bdec-55c42a835d06
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Chromecast에서 코어 재생 추적{#track-core-playback-on-chromecast}

>[!IMPORTANT]
>
>이 설명서에서는 SDK 버전 2.x의 추적을 다룹니다. SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/sdk-implement/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

1. **초기 추적 설정**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   **`MediaObject`API 참조:**

   [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>); 
   ```

   **`StreamType`상수:**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`상수:**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **비디오 메타데이터 첨부**

   선택적으로 컨텍스트 데이터 변수를 통해 표준 및/또는 사용자 지정 비디오 메타데이터 객체를 비디오 추적 세션에 첨부할 수 있습니다.

   * **표준 비디오 메타데이터**

      [Chromecast에서 표준 메타데이터 구현](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

      >[!NOTE]
      >
      >표준 비디오 메타데이터 개체를 미디어 개체에 연결하는 것은 선택 사항입니다.

   * **사용자 지정 메타데이터**

      사용자 지정 변수의 변수 개체를 만들고 이 비디오의 데이터로 채웁니다. 예:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```

1. **재생을 시작할 의도 추적**

   미디어 세션 추적을 시작하려면 [개체에서 trackSessionStart](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart) `media` 를 호출합니다.

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` 재생의 시작이 아니라 재생 의도를 추적합니다. 이 API는 비디오 데이터/메타데이터를 로드하고, QoS 지표(`trackSessionStart`와 `trackPlay` 사이의 기간)를 시작할 시간을 예상하는 데 사용됩니다.

   >[!NOTE]
   >
   >두 번째 값은 2단계에서 만든 사용자 지정 비디오 메타데이터 개체 이름입니다. If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **실제 재생 시작 추적**

   Identify the event from the video player for the beginning of the video playback, where the first frame of the video is rendered on the screen, and call [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay)

   ```
   ADBMobile.media.trackPlay();
   ```

1. **재생 완료 추적**

   Identify the event from the video player for the completion of the video playback, where the user has watched the content until the end, and call [trackComplete:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackComplete();
   ```

1. **세션의 끝 추적**

   Identify the event from the video player for the unloading/closing of the video playback, where the user closes the video and/or the video is completed and has been unloaded, and call [trackSessionEnd:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd)

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` 비디오 추적 세션의 끝을 표시합니다. 세션을 끝까지 성공적으로 시청한 경우, 즉, 사용자가 끝까지 컨텐츠를 시청한 경우 `trackComplete`가 `trackSessionEnd` 전에 호출되는지 확인합니다. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **가능한 모든 일시 중지 시나리오 추적**

   Identify the event from the video player for video pause and call [trackPause:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause)

   ```
   ADBMobile.media.trackPause();
   ```

   **시나리오 일시 중지**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. 다음 시나리오에서는 모두 앱 호출 `trackPause()`가 필요합니다.

   * 사용자가 앱에서 일시 정지를 명시적으로 누릅니다.
   * 플레이어가 일시 정지 상태로 전환합니다.
   * (*모바일 앱*) - 백그라운드로 전환된 애플리케이션의 세션을 열어 두려고 합니다.
   * (*모바일 앱*) - 애플리케이션을 백그라운드로 전환하는 시스템 인터럽트 유형이 발생합니다. 예를 들어 사용자가 호출을 받거나 다른 애플리케이션에서 팝업이 발생하지만 애플리케이션이 중단 지점에서 사용자가 비디오를 재개할 수 있도록 세션을 라이브로 유지할 수 있습니다.

1. Identify the event from the player for video play and/or video resume from pause and call [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >이는 4단계에서 사용된 것과 동일한 이벤트 소스일 수 있습니다. 비디오 재생이 다시 시작될 때 각 `trackPause()` API 호출이 다음 `trackPlay()` API 호출과 연결되는지 확인하십시오.

* 추적 시나리오: [광고가 없는 VOD 재생](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* 전체 추적 예를 제공하기 위해 Chromecast SDK에 포함된 샘플 플레이어.

