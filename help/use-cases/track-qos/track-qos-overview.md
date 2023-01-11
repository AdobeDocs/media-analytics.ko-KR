---
title: 체감 품질 추적 설명
description: Media SDK를 사용한 체감 품질(QoE, QoS) 추적에 대한 개요입니다.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '258'
ht-degree: 100%

---

# 개요{#overview}

다음은 모든 2.x SDK에 구현과 관련된 지침입니다.

>[!IMPORTANT]
>
>SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/getting-started/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

체감 품질 추적에 QoS(서비스 품질) 및 오류 추적이 포함됩니다. 둘 다 선택적 옵션이며 코어 미디어 추적 구현에 필요하지 **않습니다**. 미디어 플레이어 API를 사용하여 QoS 및 오류 추적과 관련된 변수를 식별할 수 있습니다. 다음은 경험 추적 품질의 핵심 요소입니다.

## 플레이어 이벤트 {#player-events}

### QoS 지표 변경 사항이 있을 경우:

재생에 대해 QoS 개체 인스턴스를 생성하거나 업데이트하십시오. [QoS API 참조](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### 모든 비트율 변경 이벤트

호출 `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## QOS 구현

1. 미디어 재생 중 QOS 지표가 변경되는 시점을 식별하고 QoS 정보를 사용하여 `MediaObject`를 작성하고 새 QoS 정보를 업데이트합니다.

   QoSObject 변수:

   >[!TIP]
   >
   >다음 변수는 QoS를 추적하려는 경우에만 필요합니다.

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
   >비트율 변경 시마다 QoS 개체를 업데이트하고 비트율 변경 이벤트를 호출합니다. 이렇게 하면 가장 정확한 QoS 데이터가 제공됩니다.

다음 샘플 코드는 HTML5 미디어 플레이어에 JavaScript 2.x SDK를 사용합니다. 이 코드는 코어 미디어 재생 코드와 함께 사용해야 합니다.

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
