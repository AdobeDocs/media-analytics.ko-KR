---
title: 광고가 없는 VOD 재생
description: 광고가 포함되지 않은 VOD 재생 추적의 예를 봅니다.
uuid: ee2a1b79-2c2f-42e1-8e81-b62bbdd0d8cb
exl-id: 9e2240f0-da8d-4dcc-9d44-0f121c60d924
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '365'
ht-degree: 100%

---

# 광고가 없는 VOD 재생{#vod-playback-with-no-ads}

## 시나리오 {#scenario}

이 시나리오에는 광고가 없는 한 개의 VOD 자산이 있으며, 이 VOD는 처음부터 끝까지 한 번 재생됩니다.

| 트리거 | 하트비트 메서드 | 네트워크 호출 | 참고   |
|---|---|---|---|
| 사용자가 **[!UICONTROL 재생]** 클릭 | `trackSessionStart` | Analytics 콘텐츠 시작, 하트비트 콘텐츠 시작 | 재생을 클릭하는 사용자 또는 자동 재생 이벤트일 수 있습니다. |
| 미디어의 첫 번째 프레임 | `trackPlay` | 하트비트 콘텐츠 재생 | 이 메서드가 타이머를 트리거하며, 이 시점부터는 재생 시간 동안 10초마다 하트비트가 전송됩니다. |
| 콘텐츠 재생 |  | 콘텐츠 하트비트 |  |
| 콘텐츠가 완료됨 | `trackComplete` | 하트비트 콘텐츠 완료 | *완료*&#x200B;란 플레이헤드의 끝에 도달했음을 의미합니다. |

## 매개 변수 {#parameters}

하트비트 콘텐츠 시작 호출 시 표시되는 동일한 값의 대부분이 Adobe Analytics `Content Start` 호출 시에도 표시됩니다. Adobe에서는 많은 매개 변수를 사용하여 다양한 미디어 보고서를 채우지만, 다음 표에는 가장 중요한 매개 변수만 나열되어 있습니다.

### 하트비트 콘텐츠 시작

| 매개 변수 | 값 | 참고   |
|---|---|---|
| `s:sc:rsid` | &lt;Adobe 보고서 세트 ID> |  |
| `s:sc:tracking_server` | &lt;Analytics 추적 서버 URL> |  |
| `s:user:mid` | 설정해야 함 | 호출 `Adobe Analytics Content Start`의 중간값과 일치해야 합니다. |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:media_id` | &lt;미디어 이름> |  |
| `s:meta:*` | 옵션 | 미디어에 설정된 사용자 지정 메타데이터입니다. |

## 하트비트 콘텐츠 재생 {#heartbeat-content-play}

이러한 매개 변수는 `Heartbeat Content Start` 호출과 거의 비슷하게 보이지만, 주요한 차이점은 `s:event:type` 매개 변수입니다. 다른 모든 매개 변수는 여전히 존재해야 합니다.

| 매개 변수 | 값 | 참고   |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |

## 콘텐츠 하트비트 {#content-heartbeats}

미디어 재생 중에 타이머는 10초마다 1개 이상의 하트비트를 보냅니다. 이러한 하트비트에는 재생, 광고, 버퍼링 등에 대한 정보가 포함되어 있습니다. 각 하트비트의 정확한 콘텐츠는 이 문서의 범위를 벗어나지만 중요한 문제는 재생이 계속되는 동안 하트비트가 일관되게 트리거된다는 것입니다.

콘텐츠 하트비트에서 다음 매개 변수를 찾아 보십시오.

| 매개 변수 | 값 | 참고   |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | &lt;playhead position> 예: 50,60,70 | 이 매개 변수는 플레이헤드의 현재 위치를 반영합니다. |

## 하트비트 콘텐츠 완료 {#heartbeat-content-complete}

재생이 완료되면, 즉 플레이헤드의 끝에 도달하면 `Heartbeat Content Complete` 호출이 전송됩니다. 이 호출은 다른 하트비트 호출과 비슷해 보이지만 몇 가지 특정 매개 변수를 포함합니다.

| 매개 변수 | 값 | 참고   |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

## 샘플 코드 {#sample-code}

이 시나리오에서 콘텐츠 길이는 40초이며, 중단 없이 끝까지 재생됩니다.

![](assets/main-content-regular-playback.png)

### Android

```java
// Set up  mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay  
//    is used, i.e., there's an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts,  
//    i.e., the first frame of media is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end,  
//    i.e., when the media completes and finishes playing.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() when the playback session is over.  
//    This method must be called even if the user does not watch  
//    the media to completion.  
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

### iOS

```
when the user clicks Play 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeVOD]; 

NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 

// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there's an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 

// 2. Call trackPlay when the playback actually starts, i.e., when the  
//    first frame of main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 

// 3. Call trackComplete when the playback reaches the end, i.e.,  
//    when the media completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
........ 
........ 

// 4. Call trackSessionEnd when the playback session is over. This method  
//    must be called even if the user does not watch the media to completion. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript

```js
// Set up mediaObject 

var mediaInfo = MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME, Configuration.MEDIA_ID,  
Configuration.MEDIA_LENGTH,MediaHeartbeat.StreamType.VOD); 
var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 

}; 

// 1. Call trackSessionStart() when the user clicks play, or when autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the main content starts, i.e.,  
//    the first frame of the media content is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end,  
    i.e., the media completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() when the playback session is over.  
//    This method must be called even if the user does not  
//    watch the media to completion. 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........
```
