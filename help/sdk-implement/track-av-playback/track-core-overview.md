---
title: 추적 개요
description: '이 항목에서는 미디어 로드, 미디어 시작, 미디어 일시 중지, 미디어 완료 추적을 포함한 코어 재생 추적에 대해 설명합니다. '
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 추적 개요{#tracking-overview}

>[!IMPORTANT]
>
>이 설명서는 SDK의 버전 2.x에 있는 추적 기능에 대해 설명합니다. SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/sdk-implement/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

## 플레이어 이벤트

코어 재생 추적에는 미디어 로드, 미디어 시작, 미디어 일시 정지, 미디어 완료 추적이 포함됩니다. 필수는 아니지만 버퍼링 및 찾기 추적도 컨텐츠 재생을 추적하는 데 사용되는 핵심 구성 요소입니다. 미디어 플레이어 API에서 Media SDK 추적 호출에 부합하는 플레이어 이벤트를 식별하고, 이벤트 처리기를 코딩하여 추적 API를 호출하고 필수 변수와 선택적 변수를 채우십시오.

### 미디어 로드 시

* 미디어 개체 만들기
* 메타데이터 채우기
* `trackSessionStart`를 호출합니다. 예: `trackSessionStart(mediaObject, contextData)`

### 미디어 시작 시

* 호출 `trackPlay`

### 일시 정지/재개 시

* 호출 `trackPause`
* _재생이 다시 시작될 때_ `trackPlay` 호출

### 미디어 완료 시

* 호출 `trackComplete`

### 미디어 중단 시

* 호출 `trackSessionEnd`

### 스크러빙이 시작될 때

* 호출 `trackEvent(SeekStart)`

### 스크러빙이 종료될 때

* 호출 `trackEvent(SeekComplete)`

### 버퍼링이 시작될 때

* 호출 `trackEvent(BufferStart);`

### 버퍼링이 종료될 때

* 호출 `trackEvent(BufferComplete);`

>[!TIP]
>
>플레이헤드 위치는 설정 및 구성 코드의 일부로 설정됩니다. 자세한 `getCurrentPlayheadTime`에 대한 내용은 [개요: 일반 구현 지침](/help/sdk-implement/setup/setup-overview.md#general-implementation-guidelines)을 참조하십시오.

## 구현 {#implement}

1. **초기 추적 설정 -** 사용자가 재생 의도를 트리거하는(사용자가 재생 및/또는 자동 재생 클릭) 시점을 식별하고 컨텐츠 이름, 컨텐츠 ID, 컨텐츠 길이 및 스트림 유형에 대한 미디어 정보를 사용하여 `MediaObject` 인스턴스를 만듭니다.

   **`MediaObject`참조:**

   | 변수 이름 | 설명 | 필수 여부 |
   |---|---|---|
   | `name` | 컨텐츠 이름 | 예 |
   | `mediaid` | 컨텐츠 고유 식별자 | 예 |
   | `length` | 컨텐츠 길이 | 예 |
   | `streamType` | 스트림 유형 | 예 |
   | `mediaType` | 미디어 유형(오디오 또는 비디오 컨텐츠) | 예 |

   **`StreamType`상수:**

   | 상수 이름 | 설명 |
   |---|---|
   | `VOD` | Video on Demand에 대한 스트림 유형입니다. |
   | `LIVE` | 라이브 컨텐츠에 대한 스트림 유형입니다. |
   | `LINEAR` | 선형 컨텐츠에 대한 스트림 유형입니다. |
   | `AOD` | Audio On Demand에 대한 스트림 유형입니다. |
   | `AUDIOBOOK` | 오디오북에 대한 스트림 유형입니다. |
   | `PODCAST` | 팟캐스트에 대한 스트림 유형입니다. |

   **`MediaType`상수:**

   | 상수 이름 | 설명 |
   |---|---|
   | `Audio` | 오디오 스트림에 대한 미디어 유형입니다. |
   | `Video` | 비디오 스트림에 대한 미디어 유형입니다. |

   필요한 일반적인 형식은 `MediaObject`를 작성하는 데 `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`입니다.

1. **메타데이터 첨부 -** 원할 경우 컨텍스트 데이터 변수를 통해 표준 및/또는 사용자 지정 메타데이터 개체를 추적 세션에 첨부합니다.

   * **표준 메타데이터 -**

      >[!NOTE]
      >
      >표준 메타데이터 개체를 미디어 개체에 첨부하는 것은 선택 사항입니다.

      표준 메타데이터 개체를 인스턴스화하고, 원하는 변수를 채우고, 미디어 하트비트 개체에서 메타데이터 개체를 설정합니다.

      메타데이터의 전체 목록을 [오디오 및 비디오 매개 변수](/help/metrics-and-metadata/audio-video-parameters.md)에서 참조하십시오.

   * **사용자 지정 메타데이터 -** 사용자 지정 변수에 대한 변수 개체를 만들고, 이 컨텐츠의 데이터로 채웁니다.

1. **재생을 시작할 의도 추적 -** 세션 추적을 시작하려면 미디어 하트비트 인스턴스에서 `trackSessionStart`을 호출하십시오.

   >[!IMPORTANT]
   >
   >재생 시작이 아니라 `trackSessionStart`는 사용자의 재생 의도를 추적합니다. 이 API는 데이터/메타데이터를 로드하고, QoS 지표(`trackSessionStart`와 `trackPlay` 사이의 기간)를 시작할 시간을 예상하는 데 사용됩니다.

   >[!NOTE]
   >
   >사용자 지정 메타데이터를 사용하지 않는 경우 `trackSessionStart`의 `data` 인수에 대해 빈 개체를 보내면 됩니다.

1. **실제 재생 시작 추적 -**&#x200B;미디어 플레이어에서 컨텐츠의 첫 번째 프레임이 화면에서 렌더링되는 재생 시작에 대한 이벤트를 식별하고, `trackPlay`를 호출합니다.

1. **재생 완료 추적 -**&#x200B;미디어 플레이어에서 사용자가 컨텐츠의 끝까지 시청한 재생 완료에 대한 이벤트를 식별하고, `trackComplete`을 호출합니다.

1. **세션의 끝 추적 -**&#x200B;미디어 플레이어에서 재생 업로드/종료(사용자가 컨텐츠를 닫거나 컨텐츠가 완료되어 로드가 해제되는 상황)에 대한 이벤트를 식별하고 `trackSessionEnd`를 호출합니다.

   >[!IMPORTANT]
   >
   >추적 세션의 끝을 `trackSessionEnd`는 표시합니다. 세션을 끝까지 성공적으로 시청한 경우, 즉, 사용자가 끝까지 컨텐츠를 시청한 경우 `trackComplete`가 `trackSessionEnd` 전에 호출되는지 확인합니다. 새 추적 세션에 필요한 `trackSessionStart`를 제외하고, 다른 모든 `track*` API 호출은 `trackSessionEnd` 이후 무시됩니다.

1. **가능한 모든 일시 정지 시나리오 추적 -**&#x200B;일시 정지를 위해 미디어 플레이어에서 이벤트를 식별하고 `trackPause`를 호출합니다.

   **일시 정지 시나리오 -**&#x200B;플레이어에서 일시 정지할 시나리오를 식별하고 `trackPause`가 제대로 호출되는지 확인합니다. 다음 시나리오에서는 모두 앱 호출 `trackPause()`가 필요합니다.

   * 사용자가 앱에서 일시 정지를 명시적으로 누릅니다.
   * 플레이어가 일시 정지 상태로 전환합니다.
   * (*모바일 앱*) - 백그라운드로 전환된 애플리케이션의 세션을 열어 두려고 합니다.
   * (*모바일 앱*) - 애플리케이션을 백그라운드로 전환하는 시스템 인터럽트 유형이 발생합니다. 예를 들어 사용자가 호출을 받거나 다른 애플리케이션에서 팝업이 발생하지만 애플리케이션이 중단 지점에서 사용자가 컨텐츠를 재개할 수 있도록 세션을 종료되지 않은 상태로 유지할 수 있습니다.

1. 플레이어에서 재생 및/또는 일시 중지에서 재개를 위한 이벤트를 식별하고 `trackPlay`를 호출합니다.

   >[!TIP]
   >
   >이 이벤트 소스는 4단계에서 사용한 이벤트 소스와 같을 수 있습니다. 재생이 다시 시작될 때 각 `trackPause()` API 호출이 다음 `trackPlay()` API 호출과 연결되는지 확인하십시오.

1. 미디어 플레이어에서 재생 찾기 이벤트를 수신합니다. 찾기 시작 이벤트 알림 시 `SeekStart` 이벤트를 사용하여 찾기를 추적합니다.
1. 미디어 플레이어에서 찾기 완료 알림 시 `SeekComplete` 이벤트를 사용하여 찾기 종료를 추적합니다.
1. 미디어 플레이어에서 재생 버퍼링 이벤트를 수신하고, 버퍼 시작 이벤트 알림 시 `BufferStart` 이벤트를 사용하여 버퍼링을 추적합니다.
1. 미디어 플레이어에서 버퍼 완료 알림 시 `BufferComplete` 이벤트를 사용하여 버퍼링 종료를 추적합니다.

다음 플랫폼별 항목에서 각 단계의 예를 참조하고, SDK에 포함된 샘플 플레이어를 확인하십시오.

간단한 재생 추적 예는 HTML5 플레이어에서 JavaScript 2.x SDK의 사용을 참조하십시오.

```js
/* Call on media start */ 
if (e.type == "play") { 
 
    // Check for start of media 
    if (!sessionStarted) { 
        /* Set media info */     
        /* MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                            <MEDIA_ID>,  
                                            <MEDIA_LENGTH>, 
                                            <MEDIA_STREAMTYPE>,
                                            <MEDIA_MEDIATYPE>);*/ 
        var mediaInfo = MediaHeartbeat.createMediaObject( 
          document.getElementsByTagName('video')[0].getAttribute("name"),  
          document.getElementsByTagName('video')[0].getAttribute("id"),  
          video.duration, 
          MediaHeartbeat.StreamType.VOD); 
 
        /* Set custom context data */ 
        var customVideoMetadata = { 
            isUserLoggedIn: "false", 
            tvStation: "Sample TV station", 
            programmer: "Sample programmer" 
        }; 
 
        /* Set standard video metadata */     
        var standardVideoMetadata = {}; 
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode"; 
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show"; 
        mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,  
                           standardVideoMetadata);     
 
        // Start Session 
        this.mediaHeartbeat.trackSessionStart(mediaInfo, customVideoMetadata);    
 
        // Track play 
        this.mediaHeartbeat.trackPlay();  
        sessionStarted = true;     
 
    } else { 
        // Track play for resuming playack    
        this.mediaHeartbeat.trackPlay();  
    } 
}; 
 
/* Call on video complete */ 
if (e.type == "ended") { 
    console.log("video ended"); 
    this.mediaHeartbeat.trackComplete(); 
    this.mediaHeartbeat.trackSessionEnd(); 
    sessionStarted = false;     
}; 
 
/* Call on pause */ 
if (e.type == "pause") { 
    this.mediaHeartbeat.trackPause(); 
}; 
 
/* Call on scrub start */ 
if (e.type == "seeking") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
}; 
     
/* Call on scrub stop */ 
if (e.type == "seeked") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
}; 
 
/* Call on buffer start */ 
if (e.type == “buffering”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
}; 
 
/* Call on buffer complete */ 
if (e.type == “buffered”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
};
```

## 유효성 검사 {#validate}

구현의 유효성 검사에 대한 자세한 내용은 [유효성 검사](/help/sdk-implement/validation/validation-overview.md)를 참조하십시오.

