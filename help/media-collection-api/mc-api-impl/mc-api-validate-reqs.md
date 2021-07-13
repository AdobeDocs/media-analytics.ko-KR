---
title: 이벤트 요청 확인
description: JSON 유효성 검사 스키마를 사용하여 이벤트 요청의 유효성을 검사하는 방법을 알아봅니다.
uuid: 1fc92f21-b510-4c96-8ea2-47e819f4a96e
exl-id: a78739da-9fc9-42e3-9181-1887fb3dd357
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 90%

---

# 이벤트 요청 확인{#validating-event-requests}

각 이벤트 유형에 대한 JSON 요청 본문은 백 엔드에서 JSON 스키마를 사용하여 확인됩니다. API 호출에 대한 유효성 검사가 실패하면 HTTP 응답 본문이 오류 메시지로 채워집니다.

각 이벤트 유형에 대한 JSON 유효성 검사 스키마는 `{uri}/api/v1/schemas/{eventType}`에서 공개적으로 액세스할 수 있습니다(예: `{uri}/api/v1/schemas/sessionEnd`). 이러한 JSON 유효성 검사 스키마는 각 이벤트 유형에 대한 현재 올바른 요청 본문 매개 변수를 결정하는 절대 권한입니다.

예를 들어, `sessionStart` 유효성 검사 스키마 요청에 대한 응답은 다음 샘플처럼 표시됩니다(여기서는 읽기 쉽게 포맷이 지정됨).

```
HTTP/1.1 200 OK
Server: nginx/1.13.5
Date: Thu, 18 Jan 2018 15:44:50 GMT
Content-Type: application/json
Content-Length: 2716
Connection: keep-alive

{
  "$schema":"https://json-schema.org/draft-04/schema#",
  "id":"https://alpha.hb-api.omtrdc.net/api/v1/schemas/sessionStart",
  "definitions":
  {
    "playerTime":
    {
      "type":"object","properties":
      {
        "playhead":
        {"type":"number"},
        "ts":
        {"type":"integer"}
      },
      "required":["playhead","ts"],
      "additionalProperties":false
    },
    "eventType":
    {
      "type":"string",
      "enum":[
        "sessionStart",
        "play",
        "ping",
        "bufferStart",
        "pauseStart",
        "sessionComplete",
        "bitrateChange",
        "error",
        "adBreakStart",
        "adBreakComplete",
        "adStart",
        "adComplete",
        "adSkip",
        "sessionEnd"
      ]
    },
    "qoeData":
    {
      "type":"object","properties":
      {
        "media.qoe.bitrate":
        {"type":"integer"},
        "media.qoe.droppedFrames":
        {"type":"integer"},
        "media.qoe.framesPerSecond":
        {"type":"integer"},
        "media.qoe.timeToStart":
        {"type":"integer"}
      },
      "required":[],
      "additionalProperties":false
    },
    "customMetadata":
    {
      "type":"object",
      "patternProperties":
      {
        "^[a-zA-Z0-9_\\.]+$":
        {"type":"string"}
      },
      "additionalProperties":false
    },
    "sessionStart":
    {
      "properties":
      {
        "eventType":
        {"type":"string","enum":["sessionStart"]},
        "playerTime":
        {"$ref":"#/definitions/playerTime"},
        "params":
        {"type":"object",
          "properties":
          {
            "appInstallationId":
            {"type":"string"},
            "analytics.trackingServer":
            {"type":"string"},
            "analytics.reportSuite":
            {"type":"string"},
            <...>
            "visitor.marketingCloudOrgId"],
            "additionalProperties":false
          },
          "customMetadata":
          {"$ref":"#/definitions/customMetadata"},
          "qoeData":
          {"$ref":"#/definitions/qoeData"}
        },
        "required":["eventType","playerTime","params"],
        "additionalProperties":false
      }
    },
    "type":"object","$ref":"#/definitions/sessionStart"
  }
}
```

>[!NOTE]
>
>세션 컨텍스트는 컬렉션 계층에서 사용할 수 없으므로 세션 수준 유효성 검사가 불가능합니다.
