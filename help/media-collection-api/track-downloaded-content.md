---
seo-title: 다운로드한 컨텐츠 추적
title: 다운로드한 컨텐츠 추적
uuid: 0718689 D -9602-4 E 3 F -833 C -8297 AAE 1 D 909
translation-type: tm+mt
source-git-commit: b9298de98eeb85c0e2ea0a456c98eac479f43b51

---


# 다운로드한 컨텐츠 추적{#track-downloaded-content}

## 개요 {#section_hcy_3pk_cfb}

다운로드한 컨텐츠 기능은 사용자가 오프라인 상태일 때 미디어 소비를 추적하는 기능을 제공합니다. 예를 들어 사용자는 모바일 장치에 앱을 다운로드하고 설치합니다. 그런 다음 앱을 사용하는 컨텐츠를 장치의 로컬 저장소에 다운로드합니다. 다운로드한 이 데이터를 추적하기 위해 Adobe는 다운로드된 컨텐츠 기능을 개발했습니다. 이 기능을 사용하면 사용자가 장치의 저장소에서 컨텐츠를 재생할 때 장치의 연결에 관계없이 추적 데이터가 장치에 저장됩니다. 사용자가 재생 세션을 완료하고 장치가 온라인으로 돌아오면 저장된 추적 정보가 단일 페이로드 내의 Media Collection API 백엔드로 전송됩니다. 여기서 처리 및 보고는 미디어 수집 API에서 정상으로 진행됩니다.

대비 방법은 다음과 같습니다.

* 온라인

   이 실시간 접근 방식을 통해 미디어 플레이어는 각 플레이어 이벤트에 대한 추적 데이터를 전송하며, 10 초마다 (광고에 대해 초당 1 초) 네트워크 핑을 백엔드로 전송합니다.

* 오프라인 (다운로드 컨텐츠 기능)

   이 일괄 처리 접근 방식에서는 동일한 세션 이벤트를 생성해야 하지만, 단일 세션으로 백엔드로 전송될 때까지 장치에 저장됩니다 (아래 예 참조).

각 접근 방법에는 다음과 같은 장점과 단점이 있습니다.
* 온라인 시나리오는 실시간으로 추적됩니다. 이렇게 하려면 각 네트워크 호출 전에 연결이 필요합니다.
* 오프라인 시나리오 (다운로드한 컨텐츠 기능) 는 하나의 네트워크 연결 검사만 필요로 하며, 장치에 더 큰 메모리 풋프린트가 필요합니다.

## 구현 {#section_jhp_jpk_cfb}

### 이벤트 스키마

다운로드한 컨텐츠 기능은 단순히 오프라인 버전의 (표준) 온라인 미디어 컬렉션 API 이므로 플레이어에서 배너가 배치되고 백엔드로 보내는 이벤트 데이터는 온라인 호출을 만들 때 사용하는 것과 동일한 이벤트 스키마를 사용해야 합니다. 이러한 스키마에 대한 자세한 내용은 다음을 참조하십시오.
* [개요;](/help/media-collection-api/mc-api-overview.md)
* [이벤트 요청 확인](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### 이벤트 순서

* 일괄 페이로드의 첫 번째 이벤트는 미디어 컬렉션 API와 평상시처럼 일치해야 `sessionStart` 합니다.
* **다운로드한`media.downloaded: true`** 컨텐츠를 전송할 백엔드에`params` 표시하려면 `sessionStart` 이벤트에 표준 메타데이터 매개 변수 (키) 를 포함해야 합니다. 다운로드한 데이터를 전송할 때 이 매개 변수가 없거나 false로 설정된 경우 API는 400 응답 코드 (잘못된 요청) 를 반환합니다. 이 매개 변수는 다운로드한 컨텐츠와 라이브 컨텐츠를 백엔드로 구별합니다. (`media.downloaded: true`가 활동 상태 세션에 설정되어 있는 경우 API에서 똑같이 400 응답 코드가 발생합니다.)
* 표시되는 순서로 플레이어 이벤트를 올바르게 저장하는 것은 구현에 따라 달라집니다.

### 응답 코드

* 201 - Created: Successful Request. 데이터가 유효하고 세션이 작성되었습니다. 세션이 처리됩니다.
* 400 - Bad Request. 스키마 유효성 검사에 실패했고, 모든 데이터가 삭제되었습니다. 세션 데이터가 처리되지 않습니다.

## Adobe Analtyics와의 통합 {#section_cty_kpk_cfb}

다운로드한 컨텐츠 시나리오에 대한 Analytics 시작/닫기 호출을 계산할 때, 백엔드는 받은 첫 번째 및 마지막 이벤트의 타임스탬프이며 (시작 및 완료), 호출된 `ts.` 추가 분석 필드를 설정합니다. 이 메커니즘을 사용하면 완성된 미디어 세션을 올바른 시점에 삽입할 수 있습니다 (즉, 사용자가 며칠 동안 온라인으로 돌아오지 않더라도 미디어 세션이 실제로 컨텐츠를 본 시간에 발생한 것으로 보고됩니다). _타임스탬프 선택 사항 보고서 세트를 작성하여 Adobe Analytics 측에서 이 메커니즘을 사용 가능하도록 설정해야 합니다._ 타임스탬프 선택적 보고서 세트를 활성화하려면 [타임스탬프 선택 사항을 참조하십시오.](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

## 샘플 세션 비교 {#section_qnk_lpk_cfb}

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

### 다운로드된 컨텐츠

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

