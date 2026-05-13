---
title: 사용자 지정 링크 구현 설명
description: 스트리밍 미디어 서비스에서 사용자 지정 링크 추적을 구현하는 방법에 대해 알아봅니다.
uuid: 83315e73-20ca-4db5-9d43-33daade45a13
exl-id: ee6f931a-ef80-4ebe-8ccb-cdbf970516e6
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/5N4rGrJDjkAGzRZJj6SMElP2EJq-QZjh7JLgDoKxiOo
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 206
ht-degree: 94%

---

# 사용자 지정 링크 구현 안내서{#custom-link-implementation-guide}

사용자 지정 비디오 추적은 Analytics `appMeasurement`내에서 사용자 지정 링크 코드를 사용한 수동 링크 추적을 사용합니다.
대개 사용자 지정 비디오 링크 비디오 추적은 최소한의 비디오 측정이 필요한 플랫폼 및 디바이스에서 사용됩니다.

* JavaScript에서: `s.tl()` 함수
* 모바일 앱에서: [trackAction() Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/actions.html?lang=ko-KR), [trackAction() iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/actions.html?lang=ko-KR), [trackAction() OTT](/help/use-cases/analytics-with-ott/track-app-actions.md)
* Data Insertion API에서: [linktype 태그](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)

## 요구 사항

* 비디오 플레이어 API 이벤트 및 데이터에 대한 액세스 권한
* Analytics SDK를 사용하는 경우 스크립트를 추가하는 기능
* 데이터 삽입 API를 사용하는 경우 추적 비콘(사용자 지정 스크립팅 또는 하드코드)을 추가하는 기능

## 메타데이터

* 메타데이터는 링크 데이터의 일부로서 모든 추적 호출에 추가할 수 있습니다.
* `linkTrackVars` 및 `linkTrackEvents`를 업데이트해야 합니다.

```javascript
/* Call on video complete */

if (e.type == "ended") {  
    s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15';
    s.linkTrackEvents = 'event3';
    s.prop10 = mediaName;
    s.eVar10 = mediaName;
    s.eVar12 = "video";
    s.eVar13 = document.title;
    s.eVar15 = mediaPlayerName;
    s.events = 'event3';
    s.tl(this,'o','Video Complete');
};
```

## 사용자 지정 링크를 사용하는 이유

* 최소 전제 조건이 필요합니다.
* no-script를 비롯한 모든 플랫폼에서 작동합니다.
* 체류 시간이나 사분위와 같은 모든 계산은 사용자 지정 스크립트에서 계산해야 합니다.
* 숨겨진 라이브러리 또는 스크립트가 없어서 매우 간단합니다.
* 비디오 데이터의 각 측면을 모두 제어할 수 있습니다.

## HTML5 Player용 샘플 JavaScript

```javascript
<script type="text/javascript">
  myvideo = document.getElementById('movie');
  myvideo.addEventListener('play',myHandler,false);
  myvideo.addEventListener('seeked',myHandler,false);
  myvideo.addEventListener('seeking',myHandler,false);
  myvideo.addEventListener('pause',myHandler,false);
  myvideo.addEventListener('ended',myHandler,false);

  function myHandler(e) {
      var video = document.getElementsByTagName('video')[0];
      var mediaName="13502979:Sailing";
      var mediaLength = video.duration;
      var mediaPlayerName = "HTML5 Player";
      /*Define video offset*/
      if (video.currentTime > 0) {
          mediaOffset = Math.floor(video.currentTime);
      } else {
          mediaOffset = 0;
      };
      /*Call on video start*/
      if (e.type == "play") {
          if (mediaOffset == 0) {
              console.log(mediaPlayerName +
                ' -> start -> playhead: ' +  
                Math.floor(video.currentTime));
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15';
              s.linkTrackEvents='event2';
              s.prop10=mediaName;
              s.eVar10=mediaName;
              s.eVar12="video";
              s.eVar13=document.title;
              s.eVar15=mediaPlayerName;
              s.events='event2';
              s.tl(this,'o','Video Start');
          }
      };

      /*Call on video pause*/
      if (e.type == "pause") {
          console.log(mediaPlayerName +' -> pause -> playhead: ' + Math.floor(video.currentTime));
          if (video.currentTime != video.duration) {
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15';
              s.linkTrackEvents='event7';
              s.prop10=mediaName;
              s.eVar10=mediaName;
              s.eVar12="video";
              s.eVar13=document.title;
              s.eVar15=mediaPlayerName;
              s.events='event7';
              s.tl(this,'o','Video Pause');
          }
      };

      /*Call on video complete*/
      if (e.type == "ended") {
          console.log(mediaPlayerName +
            ' -> ended -> playhead: ' +
            Math.floor(video.currentTime));
          s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15';
          s.linkTrackEvents = 'event3';
          s.prop10= m ediaName;
          s.eVar10=mediaName;
          s.eVar12="video";
          s.eVar13=document.title;
          s.eVar15=mediaPlayerName;
          s.events='event3';
          s.tl(this,'o','Video Complete');
      };
  };
</script>
```
