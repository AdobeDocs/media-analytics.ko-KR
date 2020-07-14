---
title: 다운로드한 컨텐츠 추적
description: null
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: be68a7abf7d5fd4cc725b040583801f2308ab066
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 56%

---


# 다운로드한 컨텐츠 추적{#track-downloaded-content}

## 개요 {#overview}

다운로드한 컨텐츠 기능은 사용자가 오프라인 상태인 동안에 미디어 소비를 추적하는 기능을 제공합니다. 예를 들어 사용자가 모바일 장치에 앱을 다운로드하여 설치한 다음 앱을 사용하여 콘텐츠를 장치의 로컬 저장소에 다운로드합니다. 다운로드한 데이터를 추적하기 위해 Adobe는 다운로드된 컨텐츠 기능을 개발했습니다. 이 기능을 사용하면 사용자가 장치의 저장소에서 내용을 재생하면 추적 데이터는 장치의 연결에 관계없이 장치에 저장됩니다. 사용자가 재생 세션을 끝내고 장치가 온라인으로 돌아오면 저장된 추적 정보가 단일 페이로드 내에서 Media Collection API로 다시 전송됩니다. 그런 다음 저장된 추적 정보가 Media Collection API에서 평소대로 처리 및 보고됩니다.

다음 두 가지 방법을 대조합니다.

* 온라인

   이러한 실시간 접근 방식을 통해 미디어 플레이어는 각 플레이어 이벤트에 대한 추적 데이터를 전송하고 매 10초마다(광고의 경우 1초마다) 네트워크 호출을 백엔드로 전송합니다.

* 오프라인(다운로드한 컨텐츠 기능)

   이 일괄 처리 접근 방식에서는 동일한 세션 이벤트를 생성해야 하지만 이 세션 이벤트는 단일 세션으로 백엔드로 전송될 때까지 장치에 저장됩니다(아래 예 참조).

각 접근 방식은 다음과 같은 장점과 단점이 있습니다.
* 온라인 시나리오가 실시간으로 추적됩니다. 이를 위해서는 각 네트워크 호출 전에 연결 검사가 필요합니다.
* 오프라인 시나리오(다운로드한 컨텐츠 기능)에는 한 개의 네트워크 연결 검사가 필요할 뿐만 아니라 장치에 더 큰 메모리 풋프린트가 필요합니다.

## 구현 {#implementation}

### 지원되는 플랫폼

콘텐츠 추적은 iOS 및 Android 모바일 장치에서 지원됩니다.

### 이벤트 스키마

다운로드된 컨텐츠 기능은 (표준) 온라인 미디어 수집 API의 오프라인 버전이므로, 플레이어에서 배치하여 백엔드로 보내는 이벤트 데이터는 사용자가 온라인 호출을 할 때 사용하는 것과 동일한 이벤트 스키마를 사용해야 합니다. 이러한 스키마에 대한 자세한 내용은 다음을 참조하십시오.
* [개요;](/help/media-collection-api/mc-api-overview.md)
* [이벤트 요청 확인](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### 이벤트 순서

* 일괄 처리 페이로드의 첫 번째 이벤트는 Media Collection API를 사용할 때처럼 `sessionStart`여야 합니다.
* 다운로드한 컨텐츠를 전송하는 백 엔드를 표시하려면 **`media.downloaded: true`**를`sessionStart`이벤트의 표준 메타데이터 매개 변수(`params`키)에 포함해야 합니다. 다운로드한 데이터를 보낼 때 이 매개 변수가 없거나 거짓으로 설정되어 있으면 이 API는 400 응답 코드(잘못된 요청)를 반환합니다. 이 매개 변수는 백 엔드에 다운로드한 컨텐츠와 라이브 컨텐츠를 구별합니다. If`media.downloaded: true`is set on a live session, this will likewise result in a 400 response from the API.
* 표시되는 순서로 플레이어 이벤트를 올바르게 저장하는 것은 구현에 따라 달라집니다.

### 응답 코드

* 201 - 작성됨: 요청이 성공했습니다. 데이터가 유효하고 세션이 작성되었습니다. 세션이 처리됩니다.
* 400 - 잘못된 요청: 스키마 유효성 검사에 실패했고, 모든 데이터가 삭제되었습니다. 세션 데이터가 처리되지 않습니다.

## Adobe Analtyics와의 통합 {#integration-with-adobe-analtyics}

다운로드한 컨텐츠 시나리오에 대한 Analytics 시작/닫기 호출을 계산할 때 백 엔드는 `ts.`라는 추가 Analytics 필드를 설정합니다. 이들은 받은 첫 번째 이벤트와 마지막 이벤트(시작 및 완료)에 대한 타임스탬프입니다. 이 메커니즘을 사용하면 완료된 미디어 세션을 올바른 시점에 배치할 수 있습니다. 즉, 사용자가 며칠 동안 온라인 상태가 되지 않더라도 컨텐츠를 실제로 확인할 때 미디어 세션이 발생했다고 보고합니다. _타임스탬프 선택 사항 보고서 세트를 작성하여 Adobe Analytics 측에서 이 메커니즘을 사용 가능하도록 설정해야 합니다._ 타임스탬프 선택 사항 보고서 세트를 사용하려면 [타임스탬프 선택 사항](https://docs.adobe.com/content/help/ko-KR/analytics/admin/admin-tools/timestamp-optional.html)을 참조하십시오.

## 샘플 세션 비교 {#sample-session-comparison}

```
[url]/api/v1/sessions
```

### 온라인 컨텐츠

```
{
  eventType: "sessionStart",
  playerTime: {
    playhead: 0,  
    ts: 1529997923478},  
  params: { /* Standard metadata parameters as documented */ },  
  customMetadata: { /* Custom metadata parameters as documented */ },  
  qoeData: { /* QoE parameters as documented */ }
}
```

### 다운로드한 컨텐츠

```
[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478},  
    params:{
        "media.downloaded": true
        ...
    },
    customMetadata:{},  
    qoeData:{}
},
    {eventType: "play", playerTime:
        {playhead: 0,  ts: 1529997928174}},
    {eventType: "ping", playerTime:
        {playhead: 10, ts: 1529997937503}},
    {eventType: "ping", playerTime:
        {playhead: 20, ts: 1529997947533}},
    {eventType: "ping", playerTime:
        {playhead: 30, ts: 1529997957545},},
    {eventType: "sessionComplete", playerTime:
        {playhead: 35, ts: 1529997960559}
}]
```

## 미디어 추적기 API 참조

다운로드한 컨텐츠를 구성하는 방법에 대한 자세한 내용은 [미디어 추적기 API 참조를 참조하십시오](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#media-api-reference).
