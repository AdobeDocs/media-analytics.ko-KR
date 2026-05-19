---
title: JavaScript 3.x를 사용하여 버퍼링을 추적하는 방법에 대해 알아보기
description: 브라우저 앱(JS)에서 버퍼링 이벤트를 추적하는 방법에 대해 알아봅니다.
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Bq0X19pW-5gWyLJMkst3zlEXUjZRYm2Yw9JqxJvuTZw
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 123
ht-degree: 100%

---

# JavaScript 3.x를 사용하여 버퍼링 추적{#track-buffering-on-javascript}

다음은 모든 3.x SDK에 구현과 관련된 지침입니다.

>[!IMPORTANT]
>
>SDK의 이전 버전을 구현하는 경우, [SDK 다운로드](/help/getting-started/download-sdks.md)에서 개발자 안내서를 다운로드할 수 있습니다.

## 버퍼링 추적 상수

| 상수 이름 | 설명     |
|---|---|
| `BufferStart` | 버퍼 시작 이벤트 추적을 위한 상수 |
| `BufferComplete` | 버퍼 완료 이벤트 추적을 위한 상수 |

## 버퍼링 구현

1. 미디어 플레이어에서 재생 버퍼링 이벤트를 수신하고, 버퍼 시작 이벤트 알림 시 `BufferStart` 이벤트를 사용하여 버퍼링을 추적합니다.

   ```js
   _onBufferStart = function() {
       tracker.trackEvent(ADB.Media.Event.BufferStart);
   };
   ```

1. 미디어 플레이어에서 버퍼 완료 알림 시 `BufferComplete` 이벤트를 사용하여 버퍼링 종료를 추적합니다.

   ```js
   _onBufferComplete = function() {
       tracker.trackEvent(ADB.Media.Event.BufferComplete);
   };
   ```

자세한 내용은 추적 시나리오 [버퍼링이 있는 VOD 재생](/help/use-cases/tracking-scenarios/vod-buffering.md)을 참조하십시오.
