---
seo-title: 이벤트 요청
title: 이벤트 요청
uuid: B 237 F 0 A 0-DC 29-418 B -89 EE -04 C 596 A 27 F 39
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# 이벤트 요청{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## URI 매개 변수

`sid`: 세션 요청에서 반환된 [세션 ID.](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md)

## 요청 본문

요청 본문은 JSON 이어야 하며, 이 샘플 요청 본문과 동일한 구조를 가져야 합니다.

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "{event-type}", 
    "params": {}, 
    "qoeData": {}, 
    "customMetadata": {} 
}
```

* `playerTime` (필수입니다)
   * `playhead` - 초 단위이어야 하지만, float일 수 있습니다.
   * `ts` - 타임스탬프이며, 밀리초 단위여야 합니다.
* `eventType` (필수입니다)
* `params` (선택 사항입니다)
* `customMetadata` (옵션; 이벤트 유형에만 `adStart``chapterStart` 전송)
* `qoeData` (선택 사항입니다)

For a list of valid event types for this release, see [Event types and descriptions.](../../media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***광고 추적 -**광고 추적만`adBreak`*&#x200B;할 수 있습니다.
>
>광고 주위에 `adBreakStart` 및 `adBreakComplete` "북엔드"가 없을 경우 `adStart` 및 `adComplete` 이벤트가 무시되고, 해당 광고 기간은 기본 컨텐츠 기간으로 추적됩니다. 이 경우 Adobe Analytics에서 사용할 수 있는 집계된 데이터에 상당한 영향을 줄 수 있습니다.

## 응답

```
HTTP/1.1 204 No Content 
Server nginx/1.13.5 
Date Thu, 26 Oct 2017 19:15:24 GMT 
Connection keep-alive 
Access-Control-Allow-Origin * 
Access-Control-Allow-Methods OPTIONS,POST,PUT 
Access-Control-Allow-Headers Content-Type 
Access-Control-Expose-Headers Location
```

## HTTP 응답 코드

| HTTP 응답 코드 | 설명 | 고객 작업 항목 |
|---|---|---|
| **204** | **컨텐츠 없음.**<br/><br/>하트비트 호출이 성공했습니다. | 해당 없음 |
| **400** | **잘못된 요청.** <br/><br/>요청의 형식이 잘못되었습니다. | [JSON 유효성 검사 스키마](../../media-collection-api/mc-api-ref/mc-api-json-validation.md)에서 요청 유형을 확인하십시오. |
| **404** | **발견되지 않음.**<br/><br/>미디어 세션에 대한 세션 ID를 백엔드 서비스에서 찾을 수 없습니다. | 고객 애플리케이션은 [세션 요청](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) API를 사용하여 다른 미디어 세션을 작성하고 이에 대한 추적을 보고해야 합니다. |
| **410** | **제거됨.**<br/><br/>The media session was found in the 백엔드 service but the client can no longer report activity on it. | 고객 애플리케이션은 [세션 요청](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) API를 사용하여 다른 미디어 세션을 작성하고 이에 대한 추적을 보고해야 합니다. |
| **500** | **서버 오류** | 해당 없음 |

