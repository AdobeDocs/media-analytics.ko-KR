---
title: 비활성 세션 다시 시작
description: 비활성 세션 다시 시작을 처리하는 방법에 대해 알아봅니다.
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/KT7NfrYlagrMwAjsrbSNR8YUbj5d-ihU8AfJ6wcbgOA
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 37%

---

# 비활성 세션 다시 시작{#resuming-inactive-sessions}

## 긴 일시 중지

Media SDK는 미디어 재생이 다음 비활성 상태 중 하나에 얼마나 오래 있는지를 자동으로 추적합니다.

* 일시 정지됨
* 찾기
* 정지됨
* 버퍼링

미디어 추적 세션이 30분 이상 비활성 상태에 남아 있는 경우 세션이 자동으로 닫힙니다. 이전의 비활성 비디오 추적 세션(`trackPlay`) 이후 사용자가 다시 시작하면 미디어 하트비트가 이전에 사용한 비디오 정보와 메타데이터를 사용하여 새 비디오 세션을 자동으로 생성하고, 하트비트 다시 시작 이벤트를 보냅니다.

## 다시 시작 플래그를 사용한 장치 간 핸드오프

뷰어가 장치 간에 재생을 전송할 때(예: 휴대폰에서 TV 또는 Chromecast 수신기로 비디오 캐스팅) 단일 앱 세션 연속을 처리하는 동일한 재개 메커니즘이 적용됩니다. 각 장치는 자체 Media SDK 인스턴스를 실행하므로 핸드오프는 기본적으로 여러 세션을 생성합니다. 다시 시작 플래그를 사용하여 논리적 연속으로 연결하면 Analytics에서 결합된 보기를 별도의 미디어 시작이 아닌 하나의 참여로 보고합니다.

**구현 방법:**

1. **소스 장치**(예: 전화)에서 뷰어가 브로드캐스트를 시작하면 `trackSessionEnd`을(를) 호출합니다. `trackComplete`을(를) 호출하지 마십시오. 콘텐츠가 완료되지 않았으며 다른 장치로 이동되고 있습니다.
2. **대상 장치**(예: Chromecast)에서 다시 시작 플래그가 `true`(으)로 설정되고 원본 장치에서 사용된 동일한 콘텐츠 메타데이터(이름, ID, 길이)로 설정된 `trackSessionStart`을(를) 호출합니다. 소스 장치에서 뷰어가 꺼진 플레이헤드 위치를 전달합니다.
3. 나중에 뷰어가 재생을 소스 장치로 반환하는 경우 동일한 패턴(`trackSessionEnd`)을 대상에 대해 반복하고 `trackSessionStart`(다시 시작 플래그)를 소스에 대해 반복합니다.

다시 시작 플래그를 설정하면 Adobe Analytics은 핸드오프의 두 번째 및 후속 레그에 대해 [미디어 시작](/help/reporting/metrics/media-starts.md)이 아닌 [콘텐츠 다시 시작](/help/reporting/metrics/content-resumes.md)을 증가시킵니다. SDK 인스턴스 간에 세션 ID를 공유하는 기본 제공 메커니즘이 없으므로 다시 시작 플래그는 클라이언트측 선언입니다. 즉, 뷰어가 이전 세션을 계속하고 있음을 알 때 애플리케이션 논리에 따라 전달합니다.

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
