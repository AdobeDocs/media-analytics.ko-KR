---
title: 버퍼링이 있는 VOD 재생
description: Media SDK를 사용하여 VOD 컨텐츠를 추적하는 방법의 예를 봅니다.
uuid: 958f7692-7193-40fb-a8e7-2ff4fa805330
exl-id: 3a8f913f-cb51-45ae-ac1d-862ea1e7c994
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 92%

---

# 버퍼링이 있는 VOD 재생{#vod-playback-with-buffering}

## 시나리오 {#scenario}

이 시나리오에서는 VOD 컨텐츠가 재생될 때 버퍼링이 발생합니다.

명시하지 않은 경우, 이 시나리오의 네트워크 호출은 [광고 없이 VOD 재생](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md) 시나리오의 호출과 동일합니다.

| 트리거   | 하트비트 메서드   | 네트워크 호출   | 참고   |
|---|---|---|---|
| 사용자가 **[!UICONTROL 재생]** 클릭 | `trackSessionStart` | Analytics 콘텐츠 시작, 하트비트 콘텐츠 시작 | **[!UICONTROL 재생]**&#x200B;을 클릭하는 사용자 또는 자동 재생 이벤트일 수 있습니다. |
| 비디오의 첫 번째 프레임이 재생됨. | `trackPlay` | 하트비트 컨텐츠 재생 | 이 메서드는 타이머를 트리거합니다. 재생이 계속되는 한 10초마다 하트비트가 전송됩니다. |
| 콘텐츠가 재생됩니다. |  | 컨텐츠 하트비트 |  |
| 버퍼링이 시작됨. | `trackEvent:BufferStart` | 하트비트 버퍼 |  |
| 컨텐츠가 버퍼링됩니다. |  | 컨텐츠 하트비트 |  |
| 버퍼링이 완료됨. | `trackEvent:BufferComplete` | 하트비트 버퍼, 하트비트 재생 |  |
| 컨텐츠가 재생됩니다. |  | 컨텐츠 하트비트 |  |
| 컨텐츠 재생이 완료됨. | `trackComplete` | 하트비트 컨텐츠 완료 | 플레이헤드의 끝에 도달했습니다. |
| 세션이 끝남. | `trackSessionEnd` |  | `SessionEnd`는 보고 있는 세션의 종료를 의미합니다. 이 API는 사용자가 비디오를 끝까지 시청하지 않은 경우에도 호출해야 합니다. |

## 매개 변수 {#parameters}

### 하트비트 버퍼

| 매개 변수 | 값 | 참고 |
|---|---|---|
| `s:event:type` | `"buffer"` |  |

## 샘플 코드 {#sample-code}

이 시나리오에서는 VOD 컨텐츠가 재생될 때 버퍼링이 발생합니다.

![](assets/buffer-regular-content.png)

### Android

Android에서 이 시나리오를 보려면 다음 코드를 설정합니다.

```java
// Set up mediaObject 

MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 

); 

HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
videoMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
videoMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
_mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of the main content is rendered on the screen. 
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Track the MediaHeartbeat.Event.BufferStart event when the video player  
//    goes into the buffering state and begins to buffer content. 
_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null); 

....... 
....... 

// 4. Track the MediaHeartbeat.Event.BufferComplete event when the video player  
//    goes into the buffering state and begins to buffer content. 
_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete, null, null); 

....... 
....... 

// 5. Call trackComplete() when the playback reaches the end, i.e., when the 
//    video completes and finishes playing. 
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 6. Call trackSessionEnd() when the playback session is over. This method must  
//    be called even if the user does not watch the video to completion. 
_mediaHeartbeat.trackSessionEnd(); 

........ 
```

### iOS

iOS에서 이 시나리오를 보려면 다음 코드를 설정합니다.

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeVOD]; 
 
NSMutableDictionary *videoContextData = [[NSMutableDictionary alloc] init]; 
[videoContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[videoContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 

// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
....... 
....... 

// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay];  
....... 
....... 

// 3. Track the trackEvent:ADBMediaHeartbeatEventBufferStart event when the  
//    video player goes in buffering state and begins to buffer content. 
[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
               mediaObject:nil  
               data:nil]; 
....... 
....... 

// 4. Track the trackEvent:ADBMediaHeartbeatEventBufferComplete event when  
//    the video player goes in buffering state and begins to buffer content. 
[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
               mediaObject:nil  
               data:nil]; 
....... 
....... 

// 5. Call trackComplete when the playback reaches the end, i.e., when the 
//    video completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
....... 
....... 

// 6. Call trackSessionEnd when the playback session is over. This method must  
//    be called even if the user does not watch the video to completion. 
[_mediaHeartbeat trackSessionEnd]; 
....... 
....... 
```

### JavaScript

이 시나리오를 보려면 다음 텍스트를 입력하십시오.

```js
// Set up mediaObject 

var mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 

); 

var videoMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of the ad video is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Track event MediaHeartbeat.Event.BufferStart when the video player  
//    goes into the buffering state and begins to buffer content. 
this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 

....... 
....... 

// 4. Track the MediaHeartbeat.Event.BufferComplete event when the  
//    video player goes into the buffering state and begins to buffer content. 
this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 

....... 
....... 

// 5. Call trackComplete() when the playback reaches the end, i.e.,  
//    when playback completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 6. Call trackSessionEnd() when the playback session is over. This method must  
//    be called even if the user does not watch the video to completion. 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```
