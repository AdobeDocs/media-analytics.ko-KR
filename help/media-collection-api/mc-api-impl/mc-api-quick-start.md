---
seo-title: 빠른 시작
title: 빠른 시작
uuid: CA 20 BAD 4-2 C 8 F -406 B -833 E-B 4883 A 9 AA 534
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 빠른 시작{#quick-start}

>[!TIP]
>
>Gather the request data necessary for completing a successful [Session request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) to the Media Analytics (MA) Collection API back-end server. 요청을 수동으로 보내(`curl` 또는 Postman 등을 사용)으로 요청 데이터를 빠르게 확인할 수 있습니다. 이는 요청에 올바르지 않은 데이터 유형 또는 잘못된 정보가 있는지 여부에 대한 즉각적인 피드백을 제공합니다. [JSON 유효성 검사 스키마](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)을 사용하여 적절한 요청 데이터를 제공했는지 확인합니다.

1. Experience Cloud 애플리케이션을 실행하기 위해 제공해야 하는 다음과 같은 표준, 필수 Adobe Analytics 및 방문자 데이터를 수집합니다.

   * 방문자 Experience Cloud 조직 ID
   * 방문자 Experience Cloud 사용자 ID
   * Analytics 보고서 세트 ID
   * Analytics 추적 서버 URL

1. Create a JSON object for your `sessions` request body, containing the minimum data required for a successful call. 예:

   ```
   { 
       "playerTime": { 
           "playhead": 0, 
           "ts": 1234560890123 
       }, 
       "eventType": "sessionStart", 
       "params": { 
           "media.playerName": "sample-html5-api-player", 
           "analytics.trackingServer": "[YOUR_TS]", 
           "analytics.reportSuite": "[YOUR_RSID]", 
           "media.contentType": "VOD", 
           "media.length": 60.39333333333333, 
           "media.id": "MA Collection API Sample Player", 
           "visitor.marketingCloudOrgId": "[YOUR_ORG_ID]", 
           "visitor.marketingCloudUserId": "[YOUR_ECID]",
           "media.name": "ClickMe", 
           "media.channel": "sample-channel", 
           "media.sdkVersion": "va-api-0.0.0", 
           "analytics.enableSSL": false 
       } 
   }
   ```

   >[!NOTE]
   >
   >JSON 요청 본문에서 올바른 데이터 유형을 사용해야 합니다. E.g., `analytics.enableSSL` requires a boolean, `media.length` is numeric, etc. You can check parameter types and mandatory versus optional requirements by checking the [JSON validation schemas.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

1. 세션 요청을 MA Collection API 종단점에 보냅니다. If your request payload is invalid, identify the problem and retry until you get a `201 Created` response. `curl` 이 예에서 JSON 요청 본문은 `sample_data_session`다음과 같습니다.

   ```
   $ curl -i -d \ 
     @sample_data_session https://{uri}/api/v1/sessions \ 
     > curl.sessions.out 
   
   $ cat curl.sessions.out 
   HTTP/1.1 201 Created 
   Server: nginx/1.13.5 
   Date: Mon, 18 Dec 2017 22:34:12 GMT 
   Content-Type: application/octet-stream 
   Content-Length: 0 
   Connection: keep-alive 
   Location: /api/v1/sessions/a39c037641f[...]  # <== Session ID  
   Access-Control-Allow-Origin: * 
   Access-Control-Allow-Methods: OPTIONS,POST,PUT 
   Access-Control-Allow-Headers: Content-Type 
   Access-Control-Expose-Headers: Location
   ```

[세션 요청이](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) 성공하면 위의 것과 유사한 `201 Created` 응답이 표시됩니다. 이 응답은 위치 헤더에 세션 ID를 포함합니다. 세션 ID는 모든 후속 추적 호출에 필요하므로 응답에 중요한 정보 부분입니다. [세션 요청이](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)성공적으로 반환된 후 비디오 플레이어에서 MA API를 사용하여 비디오 추적 구현을 안전하게 진행할 수 있습니다.
