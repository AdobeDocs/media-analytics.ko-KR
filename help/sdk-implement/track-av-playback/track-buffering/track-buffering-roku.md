---
seo-title: Roku에서 버퍼링 추적
title: Roku에서 버퍼링 추적
uuid: 6666 B 270-9 AA 3-42 FF -95 A 8-F 12502022 D 47
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Roku에서 버퍼링 추적{#track-buffering-on-roku}

>[!IMPORTANT]
>
>다음은 모든 2.x SDK에 구현과 관련된 지침입니다. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../../sdk-implement/download-sdks.md)

## 버퍼링 추적 상수

| 상수 이름 | 설명     |
|---|---|
| `BufferStart` | 버퍼 시작 이벤트 추적을 위한 상수 |
| `BufferComplete` | 버퍼 완료 이벤트 추적을 위한 상수 |

## 버퍼링 구현

1. 미디어 플레이어에서 재생 버퍼링 이벤트를 수신하고, 버퍼 시작 이벤트 알림 시 `BufferStart` 이벤트를 사용하여 버퍼링을 추적합니다.

   ```
   bufferInfo = {}
   bufferContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_BUFFER_START, bufferInfo, bufferContextData)
   ```

1. 미디어 플레이어에서 버퍼 완료 알림 시 `BufferComplete` 이벤트를 사용하여 버퍼링 종료를 추적합니다.

   ```
   bufferInfo = {}
   bufferContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_BUFFER_COMPLETE, bufferInfo, bufferContextData)
   ```

자세한 내용은 추적 시나리오 [버퍼링이 있는 VOD 재생](../../../sdk-implement/tracking-scenarios/vod-buffering.md)을 참조하십시오.
