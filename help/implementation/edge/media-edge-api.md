---
title: 스트리밍 미디어용 Media Edge API 설정
description: Media Edge API를 사용하여 스트리밍 미디어 데이터를 Edge Network으로 직접 전송합니다.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 스트리밍 미디어용 Media Edge API 설정

사용자 지정 또는 지원되지 않는 런타임과 같이 웹 SDK, Mobile SDK 또는 Roku SDK을 사용할 수 없는 경우 Media Edge API를 사용하여 스트리밍 미디어 데이터를 Edge Network으로 직접 전송할 수 있습니다. API는 RESTful HTTP 호출을 사용하며 완전히 사용자 지정할 수 있습니다.

* **필수 구성 요소**: [Edge 구현 개요](overview.md)([!UICONTROL Media Analytics]이(가) 활성화된 스키마, 데이터 세트, 데이터 스트림)를 완료합니다.

## Edge Network에 미디어 이벤트 보내기

미디어 이벤트는 `configId` 쿼리 매개 변수에 의해 데이터 스트림으로 처리된 `/ee/va/v1/` 끝점으로 전송됩니다. 예를 들어 세션이 `sessionStart`에 대한 POST로 시작됩니다.

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId=<datastreamID>" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": { "name": "video-123", "playerName": "player_name", "contentType": "vod", "length": 128, "channel": "sample_channel" },
        "playhead": 0
      }
    }
  }]
}'
```

응답은 모든 후속 이벤트에 포함되어야 하는 세션 ID를 반환합니다. 전체 끝점 집합, 요청/응답 형식 및 OpenAPI 사양에 대해서는 [Media Edge API 참조](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/)를 참조하십시오.

## 미디어 이벤트 추적

정확한 페이로드는 각 [이벤트](/help/implementation/events/overview.md) 및 [변수](/help/implementation/variables/overview.md) 페이지에서 **Media Edge API** 탭을 참조하십시오.

## 다음 단계

구현이 완료되면 [Edge 구현에 대한 보고를 설정](/help/reporting/setup/edge-reporting.md)할 수 있습니다.

>[!MORELIKETHIS]
>
>* [미디어 Edge API 참조](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/)
>* [이벤트 개요](/help/implementation/events/overview.md)
>* [변수 개요](/help/implementation/variables/overview.md)
