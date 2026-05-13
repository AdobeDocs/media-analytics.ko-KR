---
title: iOS에서 찾기 추적하는 방법에 대해 알아보기
description: iOS에서 Media SDK를 사용하여 찾기 시작 및 찾기 완료 이벤트를 추적하는 방법에 대해 알아봅니다.
uuid: 1d31ae99-384f-4b4d-b557-4018db177349
exl-id: e8cb4962-2a14-4bfe-9a25-2405e503ba0b
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/JWe9oadtMZIK8INj8SJ1riBfNGIaXympyhPoyg-8umk
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 133
ht-degree: 100%

---

# iOS에서 찾기 추적{#track-seeking-on-ios}

다음은 모든 2.x SDK에 구현과 관련된 지침입니다.

>[!IMPORTANT]
>
>SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/getting-started/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

## 찾기 추적 상수

| 상수 이름 | 설명     |
|---|---|
| `ADBMediaHeartbeatEventSeekStart` | 이동 시작 이벤트 추적을 위한 상수. |
| `ADBMediaHeartbeatEventSeekComplete` | 이동 완료 이벤트 추적을 위한 상수. |

## 찾기 구현

1. 미디어 플레이어에서 재생 찾기 이벤트를 수신하고, 찾기 시작 이벤트 알림 시 `SeekStart` 이벤트를 사용하여 찾기를 추적합니다.

   ```
   - (void)onSeekStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. 미디어 플레이어에서 찾기 완료 알림 시 `SeekComplete` 이벤트를 사용하여 찾기 종료를 추적합니다.

   ```
   - (void)onSeekComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

자세한 내용은 추적 시나리오 [주 콘텐츠에서 찾기를 사용하여 VOD 재생](/help/use-cases/tracking-scenarios/vod-seeking.md)을 참조하십시오.
