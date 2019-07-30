---
seo-title: 개요
title: 개요
uuid: c 14 bdbef -5846-4 d 31-8 a 14-8 e 9 e 0 e 9 c 9861
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 개요{#overview}

Media Collection API는 고객 측 Media SDK에 대한 Adobe의 RESTful 대안입니다. Media Collection API를 사용하면 플레이어에서 RESTful HTTP 호출을 사용하여 오디오 및 비디오 이벤트를 추적할 수 있습니다. 미디어 컬렉션 API는 미디어 SDK의 동일한 실시간 추적 기능과 한 가지 추가 기능을 제공합니다.

* **다운로드된 컨텐츠 추적**

   이 기능은 사용자가 온라인으로 돌아올 때까지 이벤트 데이터의 로컬 저장을 통해 오프라인 상태일 때 미디어를 추적하는 기능을 제공합니다. (자세한 내용은 [다운로드한 컨텐츠 추적](track-downloaded-content.md)을 참조하십시오.)

Media Collection API는 본질적으로 Media SDK의 서버 측 버전 역할을 하는 어댑터입니다. 즉, 미디어 SDK 설명서의 일부 측면도 미디어 컬렉션 API와 관련이 있음을 의미합니다. For example, both solutions use the same [Audio and Video Parameters](/help/metrics-and-metadata/audio-video-parameters.md), and the collected Audio and Video tracking data leads to the same [Reporting and Analysis.](/help/media-reports/media-reports-enable.md)

## 미디어 추적 데이터 흐름 {#section_pwq_n34_qbb}

미디어 수집 API를 구현하는 미디어 플레이어는 restful API 추적 호출을 미디어 추적 백엔드 서버로 직접 호출하며, 미디어 SDK를 구현하는 플레이어는 플레이어 앱 내에서 SDK API에 대한 추적 호출을 수행합니다. 웹을 통해 호출하면 Media Collection API를 구현하는 플레이어가 Media SDK에서 자동으로 처리하는 과정의 일부를 처리해야 합니다. (Details in [Media Collection Implementation.](mc-api-impl/mc-api-quick-start.md))

미디어 수집 API로 캡처한 추적 데이터는 미디어 SDK 플레이어에서 캡처한 추적 데이터와 다르게 전송되어 처음 처리되지만, 백엔드 처리 엔진은 두 솔루션에 모두 사용됩니다.

![](assets/col_api_overview_simple.png)

## API Overview {#section_y4n_mcl_kcb}

**URI:** Adobe 담당자에게서 얻습니다.

**HTTP 메서드:** JSON 요청 본문이 있는 POST.

### API 호출 {#mc-api-calls}

* **`sessions`-** with a session with the server, and return a session id used in subsequent `events` call. 앱에서 추적 세션이 시작될 때 이 ID를 한 번 호출합니다.

   ```
   {uri}/api/v1/sessions
   ```

* **`events`-** Media Tracking Data를 전송합니다.

   ```
   {uri}/api/v1/sessions/{session-id}/events
   ```

### 요청 본문 {#mc-api-request-body}

```
{ 
    "playerTime": { 
        "playhead": {playhead position in seconds}, 
        "ts": {timestamp in milliseconds} 
    }, 
    "eventType": {event-type}, 
    "params": { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    }, 
    "qoeData" : { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    }, 
    "customMetadata": { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    } 
} 
```

* `playerTime` - 모든 요청에 대해 필수.
* `eventType` - 모든 요청에 대해 필수.
* `params` - 특정 `eventTypes`에 필수입니다. [JSON 유효성 검사 스키마](mc-api-ref/mc-api-json-validation.md)에서 필수 eventTypes과 옵션 eventTypes를 확인합니다.

* `qoeData` - 모든 요청의 경우 선택 사항입니다.
* `customMetadata` - 모든 요청에 대해 선택 사항이지만, 이벤트 유형과 함께 `sessionStart``adStart``chapterStart` 보내집니다.

각 `eventType`의 경우 매개 변수 유형을 확인하고 매개 변수가 특정 이벤트에 필수인지 또는 선택 사항인지 확인하는 데 사용해야 하는 [JSON 유효성 검사 스키마](mc-api-ref/mc-api-json-validation.md)가 있으며, 이 스키마는 공개적으로 제공됩니다.

### 이벤트 유형{#mc-api-event-types}을 참조하십시오 

* `sessionStart`
* `play`
* `ping`
* `pauseStart`
* `bufferStart`
* `adStart`
* `adComplete`
* `adSkip`
* `adBreakStart`
* `adBreakComplete`
* `chapterStart`
* `chapterSkip`
* `chapterComplete`
* `sessionEnd`
* `sessionComplete`

