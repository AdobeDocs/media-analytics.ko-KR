---
title: JavaScript 3.x를 사용하여 검색 추적
description: 이 항목에서는 브라우저 앱(JS)에서 Media SDK를 사용하여 찾기 추적을 구현하는 방법에 대해 설명합니다.
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 76%

---


# JavaScript 3.x를 사용하여 검색 추적{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>다음은 모든 3.x SDK에 구현과 관련된 지침입니다. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 찾기 추적 상수

| 상수 이름 | 설명     |
|---|---|
| `SeekStart` | 이동 시작 이벤트 추적을 위한 상수. |
| `SeekComplete` | 이동 완료 이벤트 추적을 위한 상수. |

## 찾기 구현

1. 미디어 플레이어에서 재생 찾기 이벤트를 수신하고, 찾기 시작 이벤트 알림 시 `SeekStart` 이벤트를 사용하여 찾기를 추적합니다.

   ```js
   _onSeekStart = function() {
       tracker.trackEvent(ADB.Media.Event.SeekStart);
   };
   ```

1. 미디어 플레이어에서 찾기 완료 알림 시 `SeekComplete` 이벤트를 사용하여 찾기 종료를 추적합니다.

   ```js
   _onSeekComplete = function() {
       tracker.trackEvent(ADB.Media.Event.SeekComplete);
   };
   ```

자세한 내용은 추적 시나리오 [주 컨텐츠에서 찾기를 사용하여 VOD 재생](/help/sdk-implement/tracking-scenarios/vod-seeking.md)을 참조하십시오.
