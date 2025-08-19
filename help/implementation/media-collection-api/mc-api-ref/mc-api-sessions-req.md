---
title: 스트리밍 미디어 서비스 API - 세션 요청 엔드포인트
description: Media Collection API 세션 요청 엔드포인트 매개 변수 및 응답은 무엇입니까?
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
exl-id: f55f5838-610f-4f82-b3c5-72165ea2c86b
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 85%

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
   * `playhead`- 콘텐츠가 라이브인 경우, 플레이헤드는 해당 요일의 현재 초여야 합니다(0 &lt;= 플레이헤드 &lt; 86,400). 콘텐츠가 기록된 경우, 플레이헤드는 콘텐츠의 현재 초여야 합니다(0 &lt;= 플레이헤드 &lt; 콘텐츠 길이). 값은 부동 소수점 숫자일 수 있습니다.
   * `ts`- 타임스탬프는 밀리초 단위이고, 협정 세계시(UTC)여야 합니다.
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
