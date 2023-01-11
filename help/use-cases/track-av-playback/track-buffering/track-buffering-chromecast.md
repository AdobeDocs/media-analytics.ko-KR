---
title: Chromecast에서 버퍼링을 추적하는 방법에 대해 알아보기
description: Chromecast에서 버퍼링 이벤트를 추적하는 방법에 대해 알아보십시오.
uuid: f6fa3a1a-d7de-4293-bd11-ebe9e130badd
exl-id: 26fd1e2a-4103-486f-be12-36b088d28cb6
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '133'
ht-degree: 100%

---

# Chromecast에서 버퍼링 추적{#track-buffering-on-chromecast}

다음은 모든 2.x SDK에 구현과 관련된 지침입니다.

>[!IMPORTANT]
>
>SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/getting-started/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

## 버퍼링 추적 상수


| 상수 이름 | 설명     |
|---|---|
| `BufferStart` | 버퍼 시작 이벤트 추적을 위한 상수 |
| `BufferComplete` | 버퍼 완료 이벤트 추적을 위한 상수 |

## 버퍼링 구현

1. 미디어 플레이어에서 재생 버퍼링 이벤트를 수신하고, 버퍼 시작 이벤트 알림 시 `BufferStart` 이벤트를 사용하여 버퍼링을 추적합니다([trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)).

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);
   ```

1. 미디어 플레이어에서 버퍼 완료 알림 시 `BufferComplete` 이벤트를 사용하여 버퍼링 종료를 추적합니다([trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)).

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
   ```

자세한 내용은 추적 시나리오 [버퍼링이 있는 VOD 재생](/help/use-cases/tracking-scenarios/vod-buffering.md)을 참조하십시오.
