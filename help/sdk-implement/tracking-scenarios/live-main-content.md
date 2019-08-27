---
seo-title: 라이브 주 컨텐츠
title: 라이브 주 컨텐츠
uuid: E 92 E 99 F 4-C 395-48 AA -8 A 30-CBDD 2 F 5 FC 07 C
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# 라이브 주 컨텐츠{#live-main-content}

## 시나리오 {#section_13BD203CBF7546D2A6AD0129B1EEB735}

이 시나리오에는 라이브 스트림에 참여한 후 40초 동안 광고가 재생되지 않는 라이브 자산이 한 개 있습니다.

| 트리거 | 하트비트 메서드 | 네트워크 호출 | 참고   |
|---|---|---|---|
| User clicks **[!UICONTROL Play]** | `trackSessionStart` | Analytics 컨텐츠 시작, 하트비트 컨텐츠 시작 | **[!UICONTROL 재생]을 클릭하는 사용자 또는 자동 재생 이벤트일 수 있습니다.** |
| 미디어의 첫 번째 프레임이 재생됩니다. | `trackPlay` | 하트비트 컨텐츠 재생 | 이 메서드는 타이머를 트리거합니다. 하트비트는 재생이 계속되는 한 10초마다 전송됩니다. |
| 컨텐츠가 재생됨. |  | 컨텐츠 하트비트 |  |
| 세션이 끝남. | `trackSessionEnd` |  | `SessionEnd`는 보고 있는 세션의 종료를 의미합니다. 사용자가 미디어를 완료로 소비하지 않더라도 이 API를 호출해야 합니다. |

## 매개 변수 {#section_D52B325B99DA42108EF560873907E02C}

Adobe Analytics 컨텐츠 시작 호출 시 표시되는 같은 값의 대부분이 하트비트 컨텐츠 시작 호출 시에도 표시됩니다. Adobe Analytics에서 다양한 미디어 보고서를 채우는 데 사용하는 다른 매개 변수가 많이 표시됩니다. 여기서 그러한 모든 내용을 다루지는 않으며, 실제로 중요한 내용만 다룹니다.

### 하트비트 컨텐츠 시작

| 매개 변수 | 값 | 참고 |
|---|---|---|
| `s:sc:rsid` | &lt;Adobe 보고서 세트 ID&gt; |  |
| `s:sc:tracking_serve` | &lt;Analytics 추적 서버 URL&gt; |  |
| `s:user:mid` | `s:user:mid` | Adobe Analytics 컨텐츠 시작 호출 시 mid 값과 일치해야 함 |
| `s:event:type` | "시작" |  |
| `s:asset:type` | "main" |  |
| `s:asset:mediao_id` | &lt; 사용자 미디어 이름 &gt; |  |
| `s:stream:type` | live |  |
| `s:meta:*` | 옵션 | 미디어에 사용자 정의 메타데이터 설정 |

## 컨텐츠 하트비트 {#section_7B387303851A43E5993F937AE2B146FE}

미디어 재생 중에 메인 컨텐츠의 경우 10 초마다 하트비트 (또는 ping) 를 하나 이상 보내는 타이머가 있고, 광고에 대해서는 매 초 동안 전송됩니다. 이러한 하트비트에는 재생, 광고, 버퍼링 및 기타 여러 가지에 대한 정보가 포함되어 있습니다. 각 하트비트에 대한 정확한 내용은 이 문서 범위를 벗어나며, 재생이 계속되는 동안 하트비트가 일관되게 트리거되는지 확인하는 것이 중요합니다.

컨텐츠 하트비트에서 다음 몇 가지 특정 항목을 찾으십시오.

| 매개 변수 | 값 | 참고 |
|---|---|---|
| `s:event:type` | "play" |  |
| `l:event:playhead` | &lt;playhead position&gt; 예: 50, 60, 70 | 플레이헤드의 현재 위치를 반영해야 합니다. |

## 하트비트 컨텐츠 완료 {#section_2CA970213AF2457195901A93FC9D4D0D}

라이브 스트림은 절대 완료되지 않았으므로 이 시나리오에서는 전체 호출이 없습니다.

## 재생헤드 값 설정

라이브 스트림의 경우 프로그래밍을 시작할 때부터 오프셋으로 재생헤드를 설정해야 합니다. 따라서 분석가는 사용자가 참여하는 시점에서 24 시간 동안 라이브 스트림을 종료하는 시점을 파악할 수 있습니다.

### at start

라이브 미디어의 경우 사용자가 스트림 재생을 시작할 때 현재 오프셋을 초 단위로 설정해야 `l:event:playhead` 합니다. 재생 헤드를 "0" 로 설정하는 VOD 와는 다릅니다.

예를 들어 실시간 스트리밍 이벤트는 자정에 시작되고 24 시간 동안 실행됩니다 (`a.media.length=86400`; `l:asset:length=86400`). 그런 다음 사용자가 오후 12 시에 해당 라이브 스트림을 재생한다고 가정해 보십시오. 이 시나리오에서는 43200 (12 시간) 로 설정해야 `l:event:playhead` 합니다.

### 일시 중지 시

사용자가 재생을 일시 중지하면 재생 시작에 적용된 동일한 "실시간 재생 헤드" 로직이 적용되어야 합니다. 사용자가 라이브 스트림 재생으로 돌아오면 `l:event:playhead` 사용자가 라이브 스트림을 일시 중지한 지점이 _아니라_ 새로운 오프셋 재생 헤드 위치로 값을 설정해야 합니다.

## 샘플 코드 {#section_vct_j2j_x2b}

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

