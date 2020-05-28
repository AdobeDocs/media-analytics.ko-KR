---
title: JavaScript 3.x를 사용하여 표준 메타데이터 구현
description: 브라우저 앱(JS)에서 추적 호출을 사용하여 전송할 표준 비디오 및 광고 메타데이터를 설정하는 방법을 설명합니다.
translation-type: tm+mt
source-git-commit: 8235fee973623c168dbf83f43aa85f13b4e06cff
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 46%

---


# JavaScript 3.x를 사용하여 표준 메타데이터 구현{#implement-standard-metadata-on-javascript}

## 구현

컨텍스트 데이터 개체를 인스턴스화하고 원하는 표준 메타데이터 변수를 채웁니다. 예:

```js
_onVideoLoad = function () {
    //Create the Media Object
    var mediaObject =
      ADB.Media.createMediaObject(<MEDIA_NAME>,
                                       <MEDIA_ID,
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var contextData = {};
    contextData[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show";
    contextData[MediaHeartbeat.VideoMetadataKeys.SEASON] = "Sample Season";
    contextData[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode";

    //Set standard Audio Metadata
    var contextData = {};
    contextData[MediaHeartbeat.AudioMetadataKeys.ARTIST] = "Sample Artist";
    contextData[MediaHeartbeat.AudioMetadataKeys.ALBUM] = "Sample Album";
    contextData[MediaHeartbeat.AudioMetadataKeys.LABEL] = "Sample Label";

    this._mediaHeartbeat.trackSessionStart(mediaObject, contextData);
};
```
