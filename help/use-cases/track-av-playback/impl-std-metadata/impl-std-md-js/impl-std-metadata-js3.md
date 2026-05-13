---
title: JavaScript 3.x를 사용하여 표준 메타데이터를 구현하는 방법에 대해 알아보기
description: 브라우저 앱(JS 3.x)에서 추적 호출을 사용하여 전송할 표준 비디오 및 광고 메타데이터를 설정하는 방법에 대해 알아봅니다.
exl-id: 228ba000-10e2-4906-8417-265a03367a9b
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/OiG917Flgrjv-P0QHnYPAyOR0A4KB7CRwJ2bOX-Jbjo
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 51
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
