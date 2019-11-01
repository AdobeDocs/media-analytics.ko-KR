---
title: 라이브 주 컨텐츠
description: Media SDK를 사용하여 라이브 컨텐츠를 추적하는 방법의 예입니다.
uuid: e92e99f4-c395-48aa-8a30-cbdd2f5fc07c
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 라이브 주 컨텐츠{#live-main-content}

## 시나리오 {#scenario}

이 시나리오에는 라이브 스트림에 참여한 후 40초 동안 광고가 재생되지 않는 라이브 자산이 한 개 있습니다.

| 트리거 | 하트비트 메서드 | 네트워크 호출 | 참고   |
|---|---|---|---|
| User clicks **[!UICONTROL Play]** | `trackSessionStart` | Analytics 컨텐츠 시작, 하트비트 컨텐츠 시작 | **[!UICONTROL 재생]을 클릭하는 사용자 또는 자동 재생 이벤트일 수 있습니다.** |
| 미디어의 첫 번째 프레임이 재생됩니다. | `trackPlay` | 하트비트 컨텐츠 재생 | 이 메서드는 타이머를 트리거합니다. 하트비트는 재생이 계속되는 한 10초마다 전송됩니다. |
| 컨텐츠가 재생됨. |  | 컨텐츠 하트비트 |  |
| 세션이 끝남. | `trackSessionEnd` |  | `SessionEnd`는 보고 있는 세션의 종료를 의미합니다. 사용자가 완료할 미디어를 사용하지 않는 경우에도 이 API를 호출해야 합니다. |

## 매개 변수 {#parameters}

Adobe Analytics 컨텐츠 시작 호출 시 표시되는 같은 값의 대부분이 하트비트 컨텐츠 시작 호출 시에도 표시됩니다. 또한 Adobe Analytics에서 다양한 미디어 보고서를 채우는 데 사용하는 다른 매개 변수도 많이 표시됩니다. 여기서 그러한 모든 내용을 다루지는 않으며, 실제로 중요한 내용만 다룹니다.

### 하트비트 컨텐츠 시작

| 매개 변수 | 값 | 참고 |
|---|---|---|
| `s:sc:rsid` | &lt;Adobe 보고서 세트 ID&gt; |  |
| `s:sc:tracking_serve` | &lt;Analytics 추적 서버 URL&gt; |  |
| `s:user:mid` | `s:user:mid` | Adobe Analytics 컨텐츠 시작 호출 시 mid 값과 일치해야 함 |
| `s:event:type` | "시작" |  |
| `s:asset:type` | "main" |  |
| `s:asset:mediao_id` | &lt;미디어 이름&gt; |  |
| `s:stream:type` | live |  |
| `s:meta:*` | 옵션 | 미디어에 설정된 사용자 정의 메타데이터 |

## 컨텐츠 하트비트 {#content-heartbeats}

미디어 재생 중에 타이머가 있어 기본 컨텐츠의 경우 10초마다 하나 이상의 하트비트(또는 핑)를 전송하고 매초마다 광고를 전송할 수 있습니다. 이러한 하트비트에는 재생, 광고, 버퍼링 및 기타 여러 가지에 대한 정보가 포함되어 있습니다. 각 하트비트에 대한 정확한 내용은 이 문서 범위를 벗어나며, 재생이 계속되는 동안 하트비트가 일관되게 트리거되는지 확인하는 것이 중요합니다.

컨텐츠 하트비트에서 다음 몇 가지 특정 항목을 찾으십시오.

| 매개 변수 | 값 | 참고 |
|---|---|---|
| `s:event:type` | "play" |  |
| `l:event:playhead` | &lt;playhead position&gt; 예: 50, 60, 70 | 플레이헤드의 현재 위치를 반영해야 합니다. |

## 하트비트 컨텐츠 완료 {#heartbeat-content-complete}

라이브 스트림이 완료되지 않았으므로 이 시나리오에서는 전체 호출이 발생하지 않습니다.

## 재생 헤드 값 설정

LIVE 스트림의 경우 프로그래밍 시작 시점의 재생 헤드를 오프셋으로 설정해야 보고에 있어 애널리스트가 사용자가 가입하고 24시간 보기 내에서 LIVE 스트림을 나가는 시점을 결정할 수 있습니다.

### 시작 시

LIVE 미디어의 경우 사용자가 스트림 재생을 시작할 때 현재 오프셋을 초 단위로 설정해야 `l:event:playhead` 합니다. 이것은 VOD와 대조적입니다. 여기서 재생 헤드를 "0"으로 설정할 수 있습니다.

예를 들어 LIVE 스트리밍 이벤트는 자정에 시작해서 24시간 동안(`a.media.length=86400`; `l:asset:length=86400`). 그러면 사용자가 오후 12시에 해당 LIVE 스트림을 재생한다고 가정합니다. 이 시나리오에서는 43200(스트림으로 12시간) `l:event:playhead` 으로 설정해야 합니다.

### 일시 중지 시

사용자가 재생을 일시 중지할 때 재생 시작 시 적용된 것과 동일한 "라이브 재생 헤드" 로직을 적용해야 합니다. 사용자가 LIVE 스트림을 재생하기 위해 돌아가면 이 `l:event:playhead` 값을 사용자가 LIVE 스트림을 일시 정지한 위치가 _아니라_ 새 오프셋 재생 헤드 위치로 설정해야 합니다.

## 샘플 코드 {#sample-code}

![](assets/live-content-playback.png)

### Android

다음은 예상 API 호출 순서입니다.

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen. 
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since the user does not watch live media to completion, there  
//    is no need to call trackComplete().  
_mediaHeartbeat.trackSessionEnd(); 
....... 
....... 
```

### iOS

다음은 예상 API 호출 순서입니다.

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
 
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
 
// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
 
// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 3. Call trackSessionEnd when user ends the playback session. Since the user  
//    does not watch live media to completion, there is no need to call  
//    trackComplete. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript

다음은 예상 API 호출 순서입니다.

```js
// Set up mediaObject 
var mediaInfo =  
MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME,  
                                 Configuration.MEDIA_ID,  
                                 Configuration.MEDIA_LENGTH,  
                                 MediaHeartbeat.StreamType.VOD); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay  
//    is used, i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since user does not watch live media to completion, there is  
//    no need to call trackComplete(). 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

