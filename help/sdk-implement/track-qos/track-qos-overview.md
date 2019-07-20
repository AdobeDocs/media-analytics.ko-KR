---
seo-title: 개요
title: 개요
uuid: 4 d 73 c 47 f-d 0 a 4-4228-9040-d 6432311 c 9 eb
translation-type: tm+mt
source-git-commit: 654aaef5d816e75429975d04c4e81ad4d4b6f706

---


# 개요{#overview}

>[!IMPORTANT]
>
>다음은 모든 2.x SDK에 구현과 관련된 지침입니다. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. 미디어 플레이어 API를 사용하여 QoS 및 오류 추적과 관련된 변수를 식별할 수 있습니다. 다음은 경험 추적 품질의 핵심 요소입니다.

## Player events {#player-events}

### QoS 지표 변경 사항이 있을 경우:

재생에 대해 QoS 개체 인스턴스를 생성하거나 업데이트하십시오. [QoS API 참조](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### 모든 비트율 변경 이벤트

호출 `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## 구현 QOS

1. Identify when any of QOS metrics change during media playback, create the `MediaObject` using the QoS information, and update the new QoS information.

   QoSObject 변수:

   >[!TIP]
   >
   >이 변수는 QoS를 추적하려는 경우에만 필요합니다.

   | 변수 | 설명 | 필수 여부 |
   | --- | --- | :---: |
   | `bitrate` | 현재 비트율 | 예 |
   | `startupTime` | 시작 시간 | 예 |
   | `fps` | FPS 값 | 예 |
   | `droppedFrames` | 드롭된 프레임 수 | 예 |

1. `getQoSObject()` 메서드가 업데이트된 최신 QoS 정보를 반환하는지 확인합니다.
1. 재생 시 비트율이 변경되면 미디어 하트비트 인스턴스에서 `BitrateChange`를 호출합니다.

   >[!IMPORTANT]
   >
   >QoS 개체를 업데이트하고 모든 비트 전송률 변경 시 비트 전송률 변경 이벤트를 호출합니다. 이렇게 하면 가장 정확한 QoS 데이터가 제공됩니다.

다음 샘플 코드는 HTML 5 미디어 플레이어용 JavaScript 2. x SDK를 사용합니다. 핵심 미디어 재생 코드와 함께 이 코드를 사용해야 합니다.

```js
var mediaDelegate = new MediaHeartbeatDelegate(); 
...  
 
// This is called periodically by MediaHeartbeat instance 
mediaDelegate.prototype.getQoSObject = function() { 
    return this.qosInfo; 
}; 
 
if (e.type == "qos_update") { 
    var qosInfo = MediaHeartbeat.createQoSObject(<BITRATE>,<STARTUP_TIME>,<FPS>,<DROPPED_FRAMES>); 
    mediaDelegate.qosInfo = qosInfo; 
}; 
 
if (e.type == "bitrate_change") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
};
```

## 유효성 검사 {#section_F3174831408947A893F7E8C15659E5AA}

### 비트율 변경

각 비트율 변경 시 하트비트 `bitrate_change` 호출이 전송됩니다.

### 오류

플레이어 오류 시 오류 값이 포함된 하트비트 오류 호출이 전송됩니다.
