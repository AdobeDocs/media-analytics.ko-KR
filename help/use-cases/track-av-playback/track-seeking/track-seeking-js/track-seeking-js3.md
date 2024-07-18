---
title: JavaScript 3.x를 사용하여 찾기 추적하는 방법에 대해 알아보기
description: 브라우저 앱(JS 3.x)에서 Media SDK를 사용하여 찾기 시작 및 찾기 완료 이벤트를 추적하는 방법에 대해 알아봅니다.
exl-id: b7152436-520e-4f38-a8ad-1027ca3f1f6c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 100%

---

# JavaScript 3.x를 사용하여 찾기 추적{#track-seeking-on-javascript}

다음은 모든 3.x SDK에 구현과 관련된 지침입니다.

>[!IMPORTANT]
>
>SDK의 이전 버전을 구현하는 경우, [SDK 다운로드](/help/getting-started/download-sdks.md)에서 개발자 안내서를 다운로드할 수 있습니다.

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

자세한 내용은 추적 시나리오 [주 콘텐츠에서 찾기를 사용하여 VOD 재생](/help/use-cases/tracking-scenarios/vod-seeking.md)을 참조하십시오.
