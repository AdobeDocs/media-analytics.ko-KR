---
title: iOS에서 버퍼링을 추적하는 방법에 대해 알아보기
description: iOS에서 버퍼링 이벤트를 추적하는 방법에 대해 알아보십시오.
uuid: 4f4db23a-489b-4b41-bb6e-393ec64d52a2
exl-id: 5f0a3c4b-7c9e-499d-98d0-6fcf316c4d9c
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 100%

---

# iOS에서 버퍼링 추적{#track-buffering-on-ios}

다음은 모든 2.x SDK에 구현과 관련된 지침입니다.

>[!IMPORTANT]
>
>SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/getting-started/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

## 버퍼링 추적 상수


| 상수 이름 | 설명     |
|---|---|
| `ADBMediaHeartbeatEventBufferStart` | 버퍼 시작 이벤트 추적을 위한 상수 |
| `ADBMediaHeartbeatEventBufferComplete` | 버퍼 완료 이벤트 추적을 위한 상수 |

## 버퍼링 구현

1. 미디어 플레이어에서 재생 버퍼링 이벤트를 수신하고, 버퍼 시작 이벤트 알림 시 `BufferStart` 이벤트를 사용하여 버퍼링을 추적합니다.

   ```
   - (void)onBufferStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. 미디어 플레이어에서 버퍼 완료 알림 시 `BufferComplete` 이벤트를 사용하여 버퍼링 종료를 추적합니다.

   ```
   - (void)onBufferComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

자세한 내용은 추적 시나리오 [버퍼링이 있는 VOD 재생](/help/use-cases/tracking-scenarios/vod-buffering.md)을 참조하십시오.
