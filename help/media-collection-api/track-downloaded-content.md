---
seo-title: 다운로드한 컨텐츠 추적
title: 다운로드한 컨텐츠 추적
uuid: 0718689 D -9602-4 E 3 F -833 C -8297 AAE 1 D 909
translation-type: tm+mt
source-git-commit: 501bbfe8b44a2a8e9b2ac2caab49b2317f9ea0f3

---


# 다운로드한 컨텐츠 추적{#track-downloaded-content}

## 개요 {#section_hcy_3pk_cfb}

Downloaded Content API에서는 사용자가 오프라인 상태인 동안에 미디어 소비를 추적하는 기능을 제공합니다. 예를 들어 사용자는 모바일 장치에 앱을 다운로드하고 설치합니다. 그런 다음 앱을 사용하는 컨텐츠를 장치의 로컬 저장소에 다운로드합니다. 이 다운로드된 데이터를 추적하기 위해 Adobe에서는 Downloaded Content API를 개발했습니다. 이 API를 사용하면 사용자가 장치의 저장소에서 컨텐츠를 재생할 때 장치의 연결 상태에 관계없이 추적 데이터가 장치에 저장됩니다. 사용자가 재생 세션을 완료하고 장치가 온라인이면 저장된 추적 정보가 단일 페이로드 내의 미디어 컬렉션 API 백엔드로 전송됩니다. 여기서, 이 API가 기반으로 하는 Media Collection API에서는 처리 및 보고가 정상적으로 진행됩니다.

대비 방법은 다음과 같습니다.

* Media Collection API

   이 실시간 접근 방식을 통해 미디어 플레이어는 각 플레이어 이벤트에 대한 추적 데이터를 전송하며, 10 초마다 (광고에 대해 초당 1 초) 네트워크 핑을 백엔드로 전송합니다.

* Downloaded Content API

   이 일괄 처리 접근 방식에서는, 동일한 세션 이벤트를 생성하되, 장치에 저장했다가 단일 세션으로 백엔드로 전송해야 합니다 (아래 예 참조).

각 접근 방식에는 장점과 단점이 있습니다. 즉, Media Collection API는 실시간으로 추적하지만 각 네트워크 호출 전에 연결 확인이 필요하고, Downloaded Content API는 하나의 네트워크 연결 확인만 필요하지만 장치에 더 큰 메모리 공간이 필요합니다.

## 구현 {#section_jhp_jpk_cfb}

### 이벤트 스키마

다운로드한 컨텐츠 API는 미디어 컬렉션 API를 기반으로 하므로 플레이어에서 배치와 센드가 필요한 이벤트 데이터는 동일한 이벤트 스키마가 미디어 컬렉션 API와 같이 사용되어야 합니다. For information on these schemas, see: [Overview;](../media-collection-api/mc-api-overview.md) and [Validating event requests.](../media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### 이벤트 순서

* 배치 페이로드의 첫 번째 이벤트는 `sessionStart`여야 합니다.
* You must include `media.downloaded: true` in the standard metadata parameters ( `params` key) on the `sessionStart` event. 이 매개 변수가 없거나 false로 설정되어 있으면 Downloaded Content API는 400 응답 코드(잘못된 요청)를 반환합니다. 즉, 백엔드는 다운로드한 컨텐츠와 라이브 컨텐츠를 구별하고 그에 따라 처리할 수 있습니다. (`media.downloaded: true`가 활동 상태 세션에 설정되어 있는 경우 Media Collection API에서 똑같이 400 응답 코드가 발생합니다.)

* 표시되는 순서로 플레이어 이벤트를 올바르게 저장하는 것은 구현에 따라 달라집니다.

### 응답 코드

* 201 - Created: Successful Request. 데이터가 유효하고 세션이 작성되었습니다. 세션이 처리됩니다.
* 400 - Bad Request. 스키마 유효성 검사에 실패했고, 모든 데이터가 삭제되었습니다. 세션 데이터가 처리되지 않습니다.

## Adobe Analtyics와의 통합 {#section_cty_kpk_cfb}

When computing the Analytics start/close calls for the downloaded content scenario, the back-end sets an extra Analytics field called `ts`. 받은 첫 번째 및 마지막 이벤트의 타임스탬프입니다 (시작 및 완료). 이 메커니즘을 사용하면 완성된 미디어 세션을 올바른 시점에 삽입할 수 있습니다 (즉, 사용자가 며칠 동안 온라인으로 돌아오지 않더라도 미디어 세션이 실제로 컨텐츠를 본 시간에 발생한 것으로 보고됩니다). *타임스탬프 선택 사항 보고서 세트*&#x200B;를 작성하여 Adobe Analytics 측에서 이 메커니즘을 사용 가능하도록 설정해야 합니다. To enable a timestamp optional report suite, see [Timestamps Optional.](https://marketing.adobe.com/resources/help/en_US/reference/timestamp-optional.html)

## 샘플 세션 비교 {#section_qnk_lpk_cfb}

```
[url]/api/v1/sessions
```

### Media Collection API

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

### Downloaded Content API

```
[{ 
    eventType: "sessionStart", 
    playerTime:{playhead: 0, ts: 1529997923478},  
    params:{
        "media.downloaded": true
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

