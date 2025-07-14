---
title: JavaScript 3.x를 사용하여 표준 메타데이터를 구현하는 방법에 대해 알아보기
description: 브라우저 앱(JS 3.x)에서 추적 호출을 사용하여 전송할 표준 비디오 및 광고 메타데이터를 설정하는 방법에 대해 알아봅니다.
exl-id: 228ba000-10e2-4906-8417-265a03367a9b
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '48'
ht-degree: 100%

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
