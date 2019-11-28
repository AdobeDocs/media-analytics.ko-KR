---
title: 빠른 시작
description: null
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 빠른 시작{#quick-start}

>[!TIP]
>
>MA(Media Analytics) Collection API 백 엔드 서버에 대한 성공적인 [세션 요청](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)을 완료하는 데 필요한 요청 데이터를 수집합니다. 요청을 수동으로 보내(`curl` 또는 Postman 등을 사용)으로 요청 데이터를 빠르게 확인할 수 있습니다. 이는 요청에 올바르지 않은 데이터 유형 또는 잘못된 정보가 있는지 여부에 대한 즉각적인 피드백을 제공합니다. [JSON 유효성 검사 스키마](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)을 사용하여 적절한 요청 데이터를 제공했는지 확인합니다.

1. Experience Cloud 애플리케이션을 실행하기 위해 제공해야 하는 다음과 같은 표준, 필수 Adobe Analytics 및 방문자 데이터를 수집합니다.

   * 방문자 Experience Cloud 조직 ID
   * 방문자 Experience Cloud 사용자 ID
   * Analytics 보고서 세트 ID
   * Analytics 추적 서버 URL

1. 성공적인 호출에 필요한 최소 데이터가 포함된 `sessions` 요청 본문에 대한 JSON 개체를 작성합니다. 예:

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
   >JSON 요청 본문에 올바른 데이터 유형을 사용해야 합니다. 예: `analytics.enableSSL`에는 부울을 사용하고, `media.length`에는 숫자를 사용해야 합니다. 매개 변수 유형과 필수 및 옵션 요구 사항을 [JSON 유효성 검사 스키마](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)를 확인하여 확인할 수 있습니다.

1. MA Collection API 끝점에 세션 요청을 보냅니다. 요청 페이로드가 올바르지 않은 경우 문제를 식별하고 `201 Created` 응답이 나타날 때까지 재시도합니다. 이 `curl` 예제에서 JSON 요청 본문은 `sample_data_session` 파일에 있습니다.

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

위와 유사한 `201 Created` 응답이 [세션 요청](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)이 성공하면 나타납니다. 이 응답은 위치 헤더에 세션 ID를 포함합니다. 세션 ID는 모든 후속 추적 호출에 필요하므로 응답에 중요한 정보 부분입니다. 성공적으로 [세션 요청](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)을 반환한 후 비디오 플레이어에서 MA API를 사용하여 비디오 추적을 구현하는 작업을 진행할 수 있습니다.
