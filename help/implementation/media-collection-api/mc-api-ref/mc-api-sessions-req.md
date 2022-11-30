---
title: 스트리밍 미디어 컬렉션 API — 세션 요청 끝점
description: "Media Collection API 세션 요청 끝점 매개 변수 및 응답이란 무엇입니까?"
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
exl-id: f55f5838-610f-4f82-b3c5-72165ea2c86b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 46%

---

# 세션 요청{#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## URI 매개 변수

없음

## 요청 본문

요청 본문은 JSON이어야 하며, 이 샘플 요청 본문과 구조가 동일해야 합니다.

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "sessionStart", 
    "params": { 
        "media.playerName": "sample-html5-api-player", 
        "analytics.trackingServer": "<your-aa-tracking-server>", 
        "analytics.reportSuite": "<your-aa-rsid>", 
        "analytics.visitorId": "<your-userId>", 
        "media.contentType": "VOD", 
        "media.length": 60.39333333333333, 
        "media.id": "MA API Sample Player", 
        "visitor.marketingCloudOrgId": "<your-org-id>", 
        "media.name": "ClickMe", 
        "media.channel": "sample-channel", 
        "media.sdkVersion": "va-api-0.0.0", 
        "analytics.enableSSL": false 
    }, 
    "customMetadata": { 
        "myCustomData": "<your metadata>", 
        "myCustomData2": "<your metadata>", 
        ... 
    }, 
    "qoeData": { 
        "param1": "<your param-value>", 
        "param2": "<your param-value>", 
        ... 
    } 
}
```

* `playerTime` (필수입니다)
   * `playhead` - 컨텐츠가 라이브 상태인 경우 플레이헤드는 하루 중 현재 두 번째 플레이헤드여야 합니다. 0 &lt;= playhead &lt; 86400. 컨텐츠가 기록되면 플레이헤드가 컨텐츠의 현재 초, 0 &lt;= playhead &lt; 컨텐츠 길이여야 합니다. 값은 부동 소수점 숫자일 수 있습니다.
   * `ts` - 타임스탬프; 밀리초 단위여야 합니다. UTC(Coordinated Universal Time).
* `eventType` (필수입니다)

   **유효한 값:** `sessionStart`
* `params` (필수입니다)
* `customMetadata` (선택 사항입니다)
* `qoeData` (선택 사항입니다)

## 응답

```
HTTP/1.1 201 Created 
Server: nginx/1.13.5 
Date: Wed, 06 Dec 2017 19:14:51 GMT 
Content-Type: application/octet-stream 
Content-Length: 0 
Location: /api/v1/sessions/bfcca2ca597a3c71bc03b4ce357833ad02b3570d262ecd0c595fcf8f2ae4df58 
Access-Control-Allow-Origin: * 
Access-Control-Allow-Methods: OPTIONS,POST,PUT 
Access-Control-Allow-Headers: Content-Type 
Access-Control-Expose-Headers: Location 
Age: 0 
Via: 1.1 wsg.sanjose08
```

`Location:` 헤더 - `/api/v1/` 부분이 API 버전을 제공합니다. `[…]sessions/` 다음 부분이 세션 ID입니다.

## 응답 코드

| HTTP 응답 코드 | 설명 |
|---|---|
| 201 | 세션이 생성됨 |
| 400 | 잘못된 요청 |
| 500 | 서버 오류 |