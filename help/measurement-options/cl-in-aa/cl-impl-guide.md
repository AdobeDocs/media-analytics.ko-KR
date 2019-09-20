---
seo-title: 사용자 지정 링크 구현 안내서
title: 사용자 지정 링크 구현 안내서
uuid: 83315e73-2 파섹
translation-type: tm+mt
source-git-commit: d325f3184932b179bbd6cde0d3e82cb2e278dd2a

---


# Custom Link Implementation Guide{#custom-link-implementation-guide}

Custom Video Tracking utilizes [manual link tracking using custom link code](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html) within Analytics `appMeasurement`. 대개 사용자 지정 비디오 링크 비디오 추적은 최소한의 비디오 측정이 필요한 플랫폼 및 장치에서 사용됩니다.

* JavaScript:함수 `s.tl()` 함수
* 모바일 앱에서: [trackAction() Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/actions.html), [trackAction() iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/actions.html), [trackAction() OTT](/help/sdk-implement/analytics-with-ott/track-app-actions.md)
* In Data Insertion API: [linktype tag](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)

## 요구 사항

* 비디오 플레이어 API 이벤트 및 데이터에 대한 액세스 권한
* Analytics SDK를 사용하는 경우 스크립트를 추가하는 기능
* Data Insertion API를 사용하는 경우 추적 비콘(사용자 지정 스크립팅 또는 하드코드)을 추가하는 기능

## 메타데이터

* 메타데이터는 링크 데이터의 일부로서 모든 추적 호출에 추가할 수 있습니다.
* Remember to update the `linkTrackVars` and `linkTrackEvents`

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
* NoScript를 비롯한 모든 플랫폼에서 작동합니다.
* 체류 시간이나 사분위와 같은 모든 계산은 사용자 지정 스크립트에서 계산해야 합니다.
* 숨겨진 라이브러리 또는 스크립트가 없어서 매우 간단합니다.
* 비디오 데이터의 각 측면을 모두 제어할 수 있습니다.
* 샘플 플레이어 링크 제거

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

