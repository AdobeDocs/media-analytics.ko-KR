---
title: 스트리밍 미디어 서비스에서 오프라인 다운로드 콘텐츠를 추적하는 방법
description: 다운로드한 콘텐츠 기능을 사용하여 사용자가 오프라인일 때 미디어 소비를 추적할 수 있습니다.
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
exl-id: 82d3e5d7-4f88-425c-8bdb-e9101fc1db92
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 98%

---

# 다운로드한 콘텐츠 추적{#track-downloaded-content}

## 개요 {#overview}

다운로드한 콘텐츠 기능은 사용자가 오프라인 상태인 동안에 미디어 소비를 추적하는 기능을 제공합니다. 예를 들어 사용자가 모바일 디바이스에 앱을 다운로드하여 설치한 다음 앱을 사용하여 콘텐츠를 디바이스의 로컬 저장소에 다운로드합니다. 다운로드한 데이터를 추적하기 위해 Adobe는 다운로드한 콘텐츠 기능을 개발했습니다. 이 기능을 사용하면 사용자가 디바이스의 저장소에서 콘텐츠를 재생할 때 디바이스의 연결 상태에 관계없이 추적 데이터가 디바이스에 저장됩니다. 사용자가 재생 세션을 마치고 디바이스가 온라인 상태이면 저장된 추적 정보는 단일 페이로드 내의 Media Collection API 백 엔드로 전송됩니다. 그런 다음 저장된 추적 정보가 Media Collection API에서 평소대로 처리 및 보고됩니다.

다음 두 가지 방법을 대조합니다.

* 온라인

  이 실시간 접근 방식을 사용하면 미디어 플레이어가 각 플레이어 이벤트에 대한 추적 데이터를 전송하고, 10초마다(광고의 경우 1초마다) 네트워크 ping을 백 엔드에 한 번에 하나씩 전송합니다.

* 오프라인 (다운로드한 콘텐츠 기능)

  배치 처리 방식을 사용하면 동일한 세션 이벤트를 생성해야 하지만, 이러한 이벤트는 단일 세션으로 백엔드에 전송될 때까지 디바이스에 저장됩니다(아래 예 참조).

각 접근 방식은 다음과 같은 장점과 단점이 있습니다.
* 온라인 시나리오가 실시간으로 추적됩니다. 이를 위해서는 각 네트워크 호출 전에 연결 검사가 필요합니다.
* 오프라인 시나리오(다운로드한 콘텐츠 기능)에는 한 개의 네트워크 연결 검사가 필요할 뿐만 아니라 디바이스에 더 큰 메모리 풋프린트가 필요합니다.

## 구현 {#implementation}

### 지원되는 플랫폼

콘텐츠 추적은 iOS 및 Android 모바일 디바이스에서 지원됩니다.

### 이벤트 스키마

다운로드한 콘텐츠 기능은 (표준) 온라인 Media Collection API의 오프라인 버전이므로, 플레이어가 이벤트 데이터를 배치 단위로 모아 백엔드로 전송할 때에도 온라인 호출 시 사용하는 것과 동일한 이벤트 스키마를 사용해야 합니다. 이들 스키마에 대한 자세한 내용은 다음을 참조하십시오.
* [개요;](/help/implementation/media-collection-api/mc-api-overview.md)
* [이벤트 요청 확인](/help/implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### 이벤트 순서

* 배치 페이로드의 첫 번째 이벤트는 Media Collection API를 사용할 때처럼 `sessionStart`여야 합니다.
* 다운로드한 콘텐츠를 전송하는 백 엔드를 표시하려면 **`media.downloaded: true`**&#x200B;를 `sessionStart` 이벤트의 표준 메타데이터 매개변수(`params` 키)에 포함해야 합니다. 다운로드한 데이터를 보낼 때 이 매개변수가 없거나 거짓으로 설정되어 있으면 이 API는 400 응답 코드(잘못된 요청)를 반환합니다. 이 매개변수는 백 엔드에 다운로드한 콘텐츠와 라이브 콘텐츠를 구별합니다. `media.downloaded: true`가 활동 상태 세션에 설정되어 있는 경우 API에서 똑같이 400 응답 코드가 발생합니다.
* 표시되는 순서로 플레이어 이벤트를 올바르게 저장하는 것은 구현에 따라 달라집니다.

### 응답 코드

* 201 - 작성됨: 요청이 성공했습니다. 데이터가 유효하고 세션이 작성되었습니다. 세션이 처리됩니다.
* 400 - 잘못된 요청: 스키마 유효성 검사에 실패했고, 모든 데이터가 삭제되었습니다. 세션 데이터가 처리되지 않습니다.

## Adobe Analytics와의 통합 {#integration-with-adobe-analtyics}

다운로드한 콘텐츠 시나리오에 대한 Analytics 시작/닫기 호출을 계산할 때 백 엔드는 `ts.`라는 추가 Analytics 필드를 설정합니다. 이들은 받은 첫 번째 이벤트와 마지막 이벤트(시작 및 완료)에 대한 타임스탬프입니다. 이 메커니즘을 사용하면 완료된 미디어 세션을 올바른 시점에 배치할 수 있습니다. 즉, 사용자가 며칠 동안 온라인 상태가 되지 않더라도 콘텐츠를 실제로 확인할 때 미디어 세션이 발생했다고 보고합니다. _타임스탬프 선택 사항 보고서 세트를 작성하여 Adobe Analytics 측에서 이 메커니즘을 사용 가능하도록 설정해야 합니다._ 타임스탬프 선택 사항 보고서 세트를 사용하려면 [타임스탬프 선택 사항](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/timestamp-optional.html?lang=ko-KR)을 참조하십시오.

## 샘플 세션 비교 {#sample-session-comparison}

### 온라인 콘텐츠

```
POST /api/v1/sessions HTTP/1.1

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

### 다운로드한 콘텐츠

```
POST /api/v1/downloaded HTTP/1.1

[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },  
    params:{...},
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

### 사용 중지 알림

>[!IMPORTANT]
>
>다운로드한 콘텐츠는 이전에 `/api/v1/sessions` API로 전송될 수도 있습니다. 다운로드한 콘텐츠를 추적하는 이 방법은 이제 **사용 중지**&#x200B;되며 **삭제**&#x200B;될 예정입니다.


`/api/v1/sessions` API는 세션 초기화 이벤트만 허용합니다.
새 API를 사용할 때 이전의 필수 `media.downloaded` 플래그는 더 이상 필요하지 않습니다.
새로운 다운로드 콘텐츠 구현을 위해 `/api/v1/downloaded` API를 사용하고 이전 API에 의존하는 기존 구현을 업데이트하는 것이 좋습니다.


```
POST /api/v1/sessions HTTP/1.1
[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },
    params:{
        "media.downloaded": true,
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

다운로드한 콘텐츠를 구성하는 방법에 대한 자세한 내용은 [미디어 추적기 API 참조](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/)를 참조하십시오.
