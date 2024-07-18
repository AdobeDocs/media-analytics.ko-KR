---
title: JavaScript v3.x를 사용하여 코어 재생을 추적하는 방법에 대해 알아보기
description: JavaScript 3.x 앱을 사용하는 브라우저에서 Media SDK를 사용하여 코어 추적을 구현하는 방법에 대해 알아봅니다.
exl-id: f3145450-82ba-4790-91a4-9d2cc97bbaa5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: c308dba2d7cf07b89bf124bd6e5f972c253c9f18
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 87%

---

# JavaScript 3.x를 사용하여 코어 재생 추적{#track-core-playback-on-javascript}

이 설명서는 SDK의 버전 3.x에 있는 추적 기능에 대해 설명합니다.

>[!IMPORTANT]
>
>SDK의 이전 버전을 구현하는 경우 [SDK 다운로드](/help/getting-started/download-sdks.md)에서 개발자 안내서를 다운로드할 수 있습니다.

1. **초기 추적 설정**

   사용자가 재생 의도를 트리거하는 시기(사용자가 재생을 클릭하거나 자동 재생이 켜짐)를 식별하고 `MediaObject` 인스턴스를 만듭니다.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | 변수 이름 | 유형 | 설명 |
   | --- | --- | --- |
   | `name` | 문자열 | 미디어 이름을 나타내는 빈 문자열이 아닙니다. |
   | `id` | 문자열 | 고유한 미디어 식별자를 나타내는 빈 문자열이 아닙니다. |
   | `length` | 숫자 | 미디어의 길이(초)를 나타내는 양수입니다. 길이를 알 수 없으면 0을 사용합니다. |
   | `streamType` | 문자열 |   |
   | `mediaType` | | 미디어 유형(오디오 또는 비디오)입니다. |

   **`StreamType`상수:**

   | 상수 이름 | 설명   |
   |---|---|
   | `VOD` | Video on Demand에 대한 스트림 유형입니다. |
   | `AOD` | Audio On Demand에 대한 스트림 유형입니다. |

   **`MediaType`상수:**

   | 상수 이름 | 설명 |
   |---|---|
   | `Audio` | 오디오 스트림에 대한 미디어 유형입니다. |
   | `Video` | 비디오 스트림에 대한 미디어 유형입니다. |

   ```
   var mediaObject = ADB.Media.createMediaObject(<MEDIA_NAME>,
                                     <MEDIA_ID,
                                     <MEDIA_LENGTH>,
                                     <STREAM_TYPE>,
                                     <MEDIA_TYPE>);
   ```

1. **메타데이터 첨부**

   원할 경우 컨텍스트 데이터 변수를 통해 표준 및/또는 사용자 지정 메타데이터 추적 세션에 첨부합니다.

   * **표준 메타데이터**

     >[!NOTE]
     >
     >표준 메타데이터 첨부는 선택 사항입니다.

      * 미디어 메타데이터 키 API 참조 - [표준 메타데이터 키 - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

        사용 가능한 메타데이터의 전체 목록을 [오디오 및 비디오 매개 변수](/help/implementation/variables/audio-video-parameters.md)에서 참조하십시오.

   * **사용자 지정 메타데이터**

     사용자 지정 변수에 대한 변수 개체를 만들고, 이 미디어의 데이터로 채웁니다. 예:

     ```js
     /* Set context data */
      var contextData = {};
     
      //Standard metadata
      contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
      contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
     
      //Custom metadata
      contextData["isUserLoggedIn"] = "false";
      contextData["tvStation"] = "Sample TV Station";
     ```

1. **재생을 시작하려는 의도 추적**

   미디어 세션 추적을 시작하려면 미디어 하트비트 인스턴스에서 `trackSessionStart`를 호출합니다.

   ```js
   var mediaObject = ADB.Media.createMediaObject("video-name",
                                                 "video-id",
                                                 60.0,
                                                 ADB.Media.StreamType.VOD,
                                                 ADB.Media.MediaType.Video);
   
   var contextData = {};
   
   //Standard metadata
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
   
   //Custom metadata
   contextData["isUserLoggedIn"] = "false";
   contextData["tvStation"] = "Sample TV Station";
   
   tracker.trackSessionStart(mediaObject, contextData);
   ```

   >[!IMPORTANT]
   >
   >재생 시작이 아니라 `trackSessionStart`는 사용자의 재생 의도를 추적합니다. 이 API는 데이터/메타데이터를 로드하고, QoS 지표(`trackSessionStart`와 `trackPlay` 사이의 기간)를 시작할 시간을 예상하는 데 사용됩니다.

   >[!NOTE]
   >
   >contextData를 사용하지 않는 경우 `trackSessionStart`의 `data` 인수에 대해 빈 개체를 보내면 됩니다.

1. **실제 재생 시작 추적**

   미디어 플레이어에서 미디어의 첫 번째 프레임이 화면에서 렌더링되는 재생 시작에 대한 이벤트를 식별하고 `trackPlay`를 호출합니다.

   ```js
   tracker.trackPlay();
   ```

1. **플레이헤드 값 업데이트**

   미디어 플레이헤드가 변경되면 `mediaUpdatePlayhead` API를 호출하여 SDK에 알립니다. <br /> VOD(video-on-demand)의 경우 값은 미디어 항목의 시작 부분부터 초 단위로 지정됩니다. <br /> 라이브 스트리밍의 경우 플레이어가 콘텐츠 지속 시간에 대한 정보를 제공하지 않으면 해당 날짜의 자정(UTC) 이후 경과된 시간(초 수)으로 값을 지정할 수 있습니다.

   ```
   tracker.updatePlayhead(position)
   ```

   >[!NOTE]
   >
   >`tracker.updatePlayhead` API를 호출할 때는 다음 사항을 고려하십시오.
   >* 진행률 마커를 사용할 경우 콘텐츠 지속 시간이 필요하며 플레이헤드는 0부터 시작하여 미디어 항목의 시작부터 초 단위로 업데이트해야 합니다.
   >* Media SDK를 사용할 때는 `tracker.updatePlayhead` API를 초당 한 번 이상 호출해야 합니다.

1. **재생 완료 추적**

   미디어 플레이어에서 사용자가 콘텐츠의 끝까지 시청한 재생 완료에 대한 이벤트를 식별하고 `trackComplete`를 호출합니다.

   ```js
   tracker.trackComplete();
   ```

1. **세션의 끝 추적**

   미디어 플레이어에서 사용자가 미디어를 닫거나 미디어가 완료 및 언로드된 재생 언로드/종료에 대한 이벤트를 식별하고 `trackSessionEnd`를 호출합니다.

   ```js
   tracker.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >추적 세션의 끝을 `trackSessionEnd`는 표시합니다. 세션을 끝까지 성공적으로 시청한 경우, 즉, 사용자가 끝까지 콘텐츠를 시청한 경우 `trackComplete`가 `trackSessionEnd` 전에 호출되는지 확인합니다. 새 추적 세션에 필요한 `trackSessionStart`를 제외하고, 다른 모든 `track*` API 호출은 `trackSessionEnd` 이후 무시됩니다.

1. **가능한 모든 일시 중지 시나리오 추적**

   미디어 플레이어에서 일시 중지 이벤트를 식별하고 `trackPause`를 호출합니다.

   ```js
   tracker.trackPause();
   ```

   **시나리오 일시 중지**

   미디어 플레이어에서 일시 중지할 시나리오를 식별하고 `trackPause`가 제대로 호출되는지 확인하십시오. 다음 시나리오에서는 모두 앱 호출 `trackPause()`가 필요합니다.

   * 사용자가 앱에서 일시 정지를 명시적으로 실행합니다.
   * 플레이어가 일시 정지 상태로 전환됩니다.
   * (*모바일 앱*) - 백그라운드로 전환된 애플리케이션의 세션을 열어 두려고 합니다.
   * (*모바일 앱*) - 애플리케이션을 백그라운드로 전환하는 시스템 인터럽트 유형이 발생합니다. 예를 들어 사용자가 호출을 받거나 다른 애플리케이션에서 팝업이 발생하지만 애플리케이션이 중단 지점에서 사용자가 미디어를 재개할 수 있도록 세션을 종료되지 않은 상태로 유지할 수 있습니다.

1. 플레이어에서 재생 및/또는 일시 중지에서 재개에 대한 이벤트를 식별하고 `trackPlay`를 호출합니다.

   ```js
   tracker.trackPlay();
   ```

   >[!TIP]
   >
   >이 이벤트 소스는 4단계에서 사용한 이벤트 소스와 같을 수 있습니다. 재생이 다시 시작될 때 각 `trackPause()` API 호출이 다음 `trackPlay()` API 호출과 연결되는지 확인하십시오.

* 추적 시나리오: [광고가 없는 VOD 재생](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* 전체 추적 예를 제공하기 위해 JavaScript SDK에 포함된 샘플 플레이어.
