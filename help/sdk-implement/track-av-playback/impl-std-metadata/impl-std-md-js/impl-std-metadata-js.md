---
title: JavaScript 2.x를 사용하여 표준 메타데이터를 구현하는 방법을 알아봅니다.
description: 브라우저 앱에서 추적 호출을 사용하여 전송할 표준 비디오 및 광고 메타데이터를 설정하는 방법을 알아봅니다(JS 2.x).
uuid: 523d29e3-0a62-40d7-ac74-da645024cdcb
exl-id: 889c294b-ac45-4e82-abb3-88ab70abbc3d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '69'
ht-degree: 50%

---

# JavaScript 2.x를 사용하여 표준 메타데이터 구현{#implement-standard-metadata-on-javascript}

## 메타데이터 상수

| 상수 이름 | 설명   |
| --- | --- |
| `StandardMediaMetadata` | 표준 메타데이터를 `MediaObject`에 첨부하기 위한 상수입니다. |

## 구현

표준 메타데이터 개체를 인스턴스화하고, 원하는 변수를 채우고, 미디어 하트비트 개체에서 메타데이터 개체를 설정합니다. 예:

```js
_onVideoLoad = function () {
    //Create the Media Object   
    var mediaInfo =  
      MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                       <MEDIA_ID,  
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show";
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SEASON] = "Sample Season";
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode";

    //Set standard Audio Metadata
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ARTIST] = "Sample Artist";
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ALBUM] = "Sample Album";
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.LABEL] = "Sample Label";

    mediaInfo.setValue(MediaObjectKey.StandardMediaMetadata, standardMediaMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```
