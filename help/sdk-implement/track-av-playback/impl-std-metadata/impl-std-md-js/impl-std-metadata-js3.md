---
title: JavaScript 3.x를 사용하여 표준 메타데이터를 구현하는 방법을 알아봅니다.
description: 브라우저 앱에서 추적 호출을 사용하여 전송할 표준 비디오 및 광고 메타데이터를 설정하는 방법을 알아봅니다(JS 3.x).
exl-id: 228ba000-10e2-4906-8417-265a03367a9b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 10%

---

# JavaScript 3.x를 사용하여 표준 메타데이터 구현{#implement-standard-metadata-on-javascript}

## 구현

컨텍스트 데이터 개체를 인스턴스화하고 원하는 표준 메타데이터 변수를 채웁니다. 예를 들어,

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
    contextData = "Sample Show";
    contextData = "Sample Season";
    contextData = "Sample Episode";

    //Set standard Audio Metadata
    var contextData = {};
    contextData = "Sample Artist";
    contextData = "Sample Album";
    contextData = "Sample Label";

    this.tracker.trackSessionStart(mediaObject, contextData);
};
```
