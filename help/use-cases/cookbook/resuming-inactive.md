---
title: 비활성 세션 다시 시작
description: 비활성 세션 다시 시작을 처리하는 방법에 대해 알아봅니다.
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 100%

---

# 비활성 세션 다시 시작{#resuming-inactive-sessions}

## 긴 일시 중지

Media SDK는 미디어 재생이 다음 비활성 상태 중 하나에 얼마나 오래 있는지를 자동으로 추적합니다.

* 일시 정지됨
* 이동
* 정지
* 버퍼링

미디어 추적 세션이 30분 이상 비활성 상태에 남아 있는 경우 세션이 자동으로 닫힙니다. 이전의 비활성 비디오 추적 세션(`trackPlay`) 이후 사용자가 다시 시작하면 미디어 하트비트가 이전에 사용한 비디오 정보와 메타데이터를 사용하여 새 비디오 세션을 자동으로 생성하고, 하트비트 다시 시작 이벤트를 보냅니다. 자세한 내용은 [오디오 및 비디오 매개 변수](/help/implementation/variables/audio-video-parameters.md)를 참조하십시오.


## 이전에 닫은 세션을 수동으로 재개

Media SDK는 애플리케이션이 닫혀 있지 않은 경우에만 세션을 자동으로 다시 시작합니다. 애플리케이션이 사용자 데이터를 저장하고 이전에 닫은 미디어를 다시 시작하는 기능이 있는 경우 다시 시작 이벤트를 수동으로 트리거할 수 있습니다. 비디오 추적 세션을 시작할 때 선택 사항인 비디오 재개됨 속성을 설정하십시오.

### Android

```java
// Set MediaHeartbeat.MediaObjectKey.mediaResumed to true
public void onmediaLoad(Observable observable, Object data) {

  // Replace <MEDIA_NAME> with the media name.
  // Replace <MEDIA_ID> with a media unique identifier.
  // Replace <MEDIA_LENGTH> with the media length.  
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
      <MEDIA_NAME>,  
      <MEDIA_ID>,  
      <MEDIA_LENGTH>,  
      MediaHeartbeat.StreamType.VOD
  );

  // Set to true if this is a resume playback scenario
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.mediaResumed, true);

  _heartbeat.trackSessionStart(mediaInfo, mediaMetadata);
}
```

### iOS

```
- (void)onMainmediaLoaded:(NSNotification *)notification {
  //Replace <MEDIA_NAME> with the media name.
  //Replace <MEDIA_ID> with a media unique identifier.
  //Replace <MEDIA_LENGTH> with the media length.     
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME>
                       mediaId:<MEDIA_ID>
                       length:<MEDIA_LENGTH>
                       streamType:ADBMediaHeartbeatStreamTypeVOD];

  //Set to YES if this user is resuming a previously closed media session
  [mediaObject setValue:@(YES) forKey:ADBMediaObjectKeymediaResumed];

  [_mediaHeartbeat trackSessionStart:mediaObject data:mediaMetadata];
}
```

### JavaScript

```js
_onmediaLoad = function () {
  // Replace <MEDIA_NAME> with the media name.
  // Replace <MEDIA_ID> with a media unique identifier.
  // Replace <MEDIA_LENGTH> with the media length.  
  var mediaObject =  
    MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,  
                                     MediaHeartbeat.StreamType.VOD);

  // Set to true if this user is resuming a previously closed media session
  mediaObject.setValue(MediaObjectKey.mediaResumed, true);
  this._mediaHeartbeat.trackSessionStart(mediaObject, contextData);
};
```
