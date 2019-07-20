---
seo-title: 세션 요청
title: 세션 요청
uuid: 9609192 D -4 F 7 F -4 FB 5-844 F-EA 89 D 47 C 4 E 30
translation-type: tm+mt
source-git-commit: f1c9f5f4cbcd4c043e1c7b4a5037c134b2bdd380

---


# 세션 요청{#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## URI 매개 변수

없음

## 요청 본문

요청 본문은 JSON 이어야 하며, 이 샘플 요청 본문과 동일한 구조를 가져야 합니다.

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
   * `playhead` - 초 단위이어야 하지만, float일 수 있습니다.
   * `ts` - 타임스탬프이며, 밀리초 단위여야 합니다.
* `eventType` (필수입니다)

   **유효한 값:**`sessionStart`
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

`Location:` 헤더 - `/api/v1/` 부분은 API 버전을 제공합니다. The part after `[…]sessions/` is the Session ID.

## 응답 코드

| HTTP 응답 코드 | 설명 |
|---|---|
| 201 | 작성된 세션 |
| 400 | 잘못된 요청 |
| 500 | 서버 오류 |

