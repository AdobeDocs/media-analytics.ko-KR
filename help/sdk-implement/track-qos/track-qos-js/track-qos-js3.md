---
title: JavaScript 3.x를 사용하여 경험 품질 추적
description: 이 항목에서는 JavaScript 3x를 사용하는 브라우저 앱에서 미디어 SDK를 사용하여 QoE, QoS(체감 품질) 추적을 구현하는 방법을 설명합니다.
translation-type: tm+mt
source-git-commit: fa161e2d41629fdfe77100d87d6a44728e23d77f
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 49%

---


# JavaScript 3.x를 사용하여 경험 품질 추적{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>다음은 모든 3.x SDK에 구현과 관련된 지침입니다. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## QOE 구현

1. Identify when the bitrate changes during media playback and create the `qoeObject` instance using the QoE information.

   QoEObject 변수:

   >[!TIP]
   >
   >다음 변수는 QoS를 추적하려는 경우에만 필요합니다.

   | 변수 | 유형 | 설명 |
   | --- | --- | --- |
   | `bitrate` | 수 | 현재 비트율 |
   | `startupTime` | 수 | 시작 시간 |
   | `fps` | 수 | FPS 값 |
   | `droppedFrames` | 수 | 드롭된 프레임 수 |

   QoE 개체 생성:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
   tracker.updateQoEObject(qoeObject);
   ```

1. 재생 시 비트율이 변경되면 미디어 하트비트 인스턴스에서 `BitrateChange`를 호출합니다:

   ```js
   _onBitrateChange = function() {
       // If the new bitrate value is available provide it to the tracker.
       var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
       tracker.updateQoEObject(qoeObject);
   
       tracker.trackEvent(ADB.Media.Event.BitrateChange);
   };
   ```

   >[!IMPORTANT]
   >
   >QoE 개체를 업데이트하고 비트 전송률 변경 이벤트를 호출합니다. 가장 정확한 QoE 데이터를 제공합니다.

1. SDK에 가장 업데이트된 QoE 정보를 제공하려면 호출 `updateQoEObject()` 방법을 확인하십시오.
1. 미디어 플레이어에 오류가 발생하여 플레이어 API에 오류 이벤트를 사용할 수 있는 경우 `trackError()`를 사용하여 오류 정보를 캡처합니다. ([개요](/help/sdk-implement/track-errors/track-errors-overview.md)를 참조하십시오.)

   >[!TIP]
   >
   >미디어 플레이어 오류를 추적해도 미디어 추적 세션이 중지되지 않습니다. 미디어 플레이어 오류로 인해 재생이 계속되지 않는 경우 `trackError()` 호출 후 `trackSessionEnd()`를 호출하여 미디어 추적 세션이 종료되었는지 확인하십시오.
