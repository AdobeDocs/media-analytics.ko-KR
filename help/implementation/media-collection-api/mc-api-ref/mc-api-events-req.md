---
title: 스트리밍 미디어 컬렉션 API - 이벤트 요청 엔드포인트
description: Media Collection API 이벤트 요청 엔드포인트 매개 변수 및 응답은 무엇입니까?
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/yFHQhj33PM209WycWdPZsV-Yi8qN1DN-DC0KyyqFK1I
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: 263
ht-degree: 70%

---

# 이벤트 요청{#events-request}

`POST https://{uri}/api/v1/sessions/{sid}/events`

## URI 매개 변수

`sid`: [세션 요청](mc-api-sessions-req.md)에서 반환된 세션 ID입니다.

## 요청 본문

요청 본문은 JSON이어야 하며, 이 샘플 요청 본문과 구조가 동일해야 합니다.

```json
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
* `customMetadata` (선택 사항이며, `adStart` 및 `chapterStart` 이벤트 유형과 함께 보냄)
* `qoeData` (선택 사항입니다)

올바른 이벤트 형식 및 SDK 단위 구현 예제에 대한 자세한 내용은 [이벤트 개요](/help/implementation/events/overview.md)를 참조하십시오.

>[!IMPORTANT]
>
>***광고 추적 -**`adBreak`* 내에서만 광고를 추적할 수 있습니다.
>
>광고 주위에 `adBreakStart` 및 `adBreakComplete` &quot;북엔드&quot;가 없을 경우 `adStart` 및 `adComplete` 이벤트가 무시되고, 해당 광고 기간은 기본 콘텐츠 기간으로 추적됩니다. 이 경우 Adobe Analytics에서 사용할 수 있는 집계된 데이터에 상당한 영향을 줄 수 있습니다.

## 응답

```text
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

| HTTP 응답 코드 | 설명 | 클라이언트 작업 항목 |
|---|---|---|
| **204** | **콘텐츠 없음.** <br/><br/>하트비트 호출이 성공했습니다. | 해당 사항 없음 |
| **400** | **잘못된 요청.** <br/><br/>요청의 형식이 잘못되었습니다. | [JSON 유효성 검사 스키마](mc-api-json-validation.md)에서 요청 유형을 확인하십시오. |
| **404** | **찾을 수 없음.** <br/><br/>미디어 세션의 세션 ID를 백 엔드 서비스에서 찾을 수 없습니다. | 클라이언트 애플리케이션은 [세션 요청](mc-api-sessions-req.md) API를 사용하여 다른 미디어 세션을 작성하고 이에 대한 추적을 보고해야 합니다. |
| **410** | **없어짐.** <br/><br/>미디어 세션이 백 엔드 서비스에서 발견되었지만 고객이 더 이상 이 세션에서 활동을 보고할 수 없습니다. | 클라이언트 애플리케이션은 [세션 요청](mc-api-sessions-req.md) API를 사용하여 다른 미디어 세션을 작성하고 이에 대한 추적을 보고해야 합니다. |
| **500** | **서버 오류** | 해당 사항 없음 |
