---
title: iOS에서 코어 재생을 추적하는 방법 알아보기
description: iOS에서 Media SDK를 사용하여 코어 추적을 구현하는 방법을 알아봅니다.
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
exl-id: 5c6b36b3-a421-45a4-a65e-4eb57513ca4a
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 95%

---

# iOS에서 코어 재생 추적{#track-core-playback-on-ios}

이 설명서는 SDK의 버전 2.x에 있는 추적 기능에 대해 설명합니다.

>[!IMPORTANT]
>SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/sdk-implement/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

1. **초기 추적 설정**

   사용자가 재생 의도를 트리거하는 시기(사용자가 재생을 클릭하거나 자동 재생이 켜짐)를 식별하고 `MediaObject` 인스턴스를 만듭니다.

   [createMediaObjectWithName API](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | 변수 이름 | 설명 | 필수 여부 |
   |---|---|---|
   | `name` | 비디오 이름 | 예 |
   | `mediaid` | 비디오 고유 식별자입니다 | 예 |
   | `length` | 비디오 길이 | 예 |
   | `streamType` | 스트림 유형(아래 _StreamType 상수_ 참조) | 예 |
   | `mediaType` | 미디어 유형(아래 _MediaType 상수_ 참조) | 예 |

   **`StreamType`상수:**

   | 상수 이름 | 설명 |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | Video on Demand에 대한 스트림 유형입니다 |
   | `ADBMediaHeartbeatStreamTypeLIVE` | 라이브 컨텐츠에 대한 스트림 유형입니다 |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | 선형 컨텐츠에 대한 스트림 유형입니다 |
   | `ADBMediaHeartbeatStreamTypeAOD` | Audio On Demand에 대한 스트림 유형입니다. |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | 오디오북에 대한 스트림 유형입니다. |
   | `ADBMediaHeartbeatStreamTypePODCAST` | 팟캐스트에 대한 스트림 유형입니다. |

   **`MediaType`상수:**

   | 상수 이름 | 설명 |
   |---|---|
   | `ADBMediaTypeAudio` | 오디오 스트림에 대한 미디어 유형입니다. |
   | `ADBMediaTypeVideo` | 비디오 스트림에 대한 미디어 유형입니다. |

   `MediaObject`를 작성하는 데 필요한 일반적인 형식:

   ```
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME>
                                          mediaId:<MEDIA_ID>
                                           length:<MEDIA_LENGTH>                       
                                       streamType:<STREAM_TYPE>
                                        mediaType: <MEDIA_TYPE>];
   ```

1. **비디오 메타데이터 첨부**

   원할 경우 컨텍스트 데이터 변수를 통해 표준 및/또는 사용자 지정 비디오 메타데이터 개체를 비디오 추적 세션에 첨부합니다.

   * **표준 비디오 메타데이터**

      * [iOS에서 표준 메타데이터 구현](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **비디오 메타데이터 키**

         [iOS 메타데이터 키](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * [오디오 및 비디오 매개 변수](/help/metrics-and-metadata/audio-video-parameters.md)에서 비디오 메타데이터에 대한 종합 목록을 참조하십시오.
      >[!NOTE]
      >
      >표준 비디오 메타데이터 개체를 미디어 개체에 첨부하는 것은 선택 사항입니다.

   * **사용자 지정 메타데이터**

      사용자 지정 변수에 대한 변수 개체를 만들고, 이 비디오의 데이터로 채웁니다. 예:

      ```
      NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
      [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
      [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
      ```


1. **재생을 시작하려는 의도 추적**

   미디어 세션 추적을 시작하려면 미디어 하트비트 인스턴스에서 `trackSessionStart`를 호출합니다.

   >[!TIP]
   >
   >두 번째 값은 2단계에서 작성한 사용자 지정 비디오 메타데이터 개체 이름입니다.

   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification {
   //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil];
       [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata];
   }
   ```

   >[!IMPORTANT]
   >
   >재생 시작이 아니라 `trackSessionStart`는 사용자의 재생 의도를 추적합니다. 이 API는 비디오 데이터/메타데이터를 로드하고, QoS 지표(`trackSessionStart`와 `trackPlay` 사이의 기간)를 시작할 시간을 예상하는 데 사용됩니다.

   >[!NOTE]
   >
   >사용자 지정 비디오 메타데이터를 사용하지 않는 경우 위의 iOS 예에서 주석 처리된 행에 표시된 대로 `trackSessionStart`의 `data` 인수에 대해 빈 개체를 보내면 됩니다.

1. **실제 재생 시작 추적**

   비디오 플레이어에서 비디오의 첫 번째 프레임이 화면에서 렌더링되는 비디오 재생 시작에 대한 이벤트를 식별하고, `trackPlay`()를 호출합니다.

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

1. **재생 완료 추적**

   비디오 플레이어에서 사용자가 컨텐츠의 끝까지 시청한 비디오 재생 완료에 대한 이벤트를 식별하고, `trackComplete`()를 호출합니다.

   ```
   - (void)onVideoComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackComplete];
   }
   ```

1. **세션의 끝 추적**

   비디오 플레이어에서 사용자가 비디오를 닫거나 비디오가 완료 및 업로드된 비디오 재생 업로드/종료에 대한 이벤트를 식별하고, `trackSessionEnd`()를 호출합니다.

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification {
       [_mediaHeartbeat trackSessionEnd];
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd`는 비디오 추적 세션의 끝을 표시합니다. 세션을 끝까지 성공적으로 시청한 경우, 즉, 사용자가 끝까지 컨텐츠를 시청한 경우 `trackComplete`가 `trackSessionEnd` 전에 호출되는지 확인합니다. 새 비디오 추적 세션에 필요한 `track*`를 제외하고, 다른 모든 `trackSessionEnd` API 호출은 `trackSessionStart` 이후 무시됩니다.

1. **가능한 모든 일시 중지 시나리오 추적**

   비디오 플레이어에서 비디오 일시 중지에 대한 이벤트를 식별하고 `trackPause`를 호출합니다.

   ```
   - (void)onVideoPause:(NSNotification *)notification {
       [_mediaHeartbeat trackPause];
   }
   ```

   **시나리오 일시 정지**

   비디오 플레이어에서 일시 정지할 시나리오를 식별하고 `trackPause`가 제대로 호출되는지 확인하십시오. 다음 시나리오에서는 모두 앱 호출 `trackPause()`가 필요합니다.

   * 사용자가 앱에서 일시 정지를 명시적으로 실행합니다.
   * 플레이어가 일시 정지 상태로 전환됩니다.
   * (*모바일 앱*) - 백그라운드로 전환된 애플리케이션의 세션을 열어 두려고 합니다.
   * (*모바일 앱*) - 애플리케이션을 백그라운드로 전환하는 시스템 인터럽트 유형이 발생합니다. 예를 들어 사용자가 호출을 받거나 다른 애플리케이션에서 팝업이 발생하지만 애플리케이션이 중단 지점에서 사용자가 비디오를 재개할 수 있도록 세션을 라이브로 유지할 수 있습니다.

1. 플레이어에서 비디오 재생 및/또는 일시 정지에서 비디오 재개에 대한 이벤트를 식별하고 `trackPlay`를 호출합니다.

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

   >[!TIP]
   >
   >이 이벤트 소스는 4단계에서 사용한 이벤트 소스와 같을 수 있습니다. 비디오 재생이 다시 시작될 때 각 `trackPause()` API 호출이 다음 `trackPlay()` API 호출과 연결되는지 확인하십시오.

코어 재생 추적에 대한 자세한 내용은 다음을 참조하십시오.

* 추적 시나리오: [광고가 없는 VOD 재생](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* 전체 추적 예를 제공하기 위해 iOS SDK에 포함된 샘플 플레이어.
