---
title: 스트리밍 미디어 컬렉션 API - 빠른 시작
description: Streaming Media API를 시작합니다. 요청 데이터를 빠르게 확인하는 방법에 대해 알아봅니다.
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
exl-id: 08bb5873-f69a-4fdd-8f27-69649b4acb17
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/F7NHDQkJVwVc-Th-blxBP8gifT7V55xLqlI1YT-pswc
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 294
ht-degree: 90%

---

# 빠른 시작{#quick-start}

>[!TIP]
>
>MA(Media Analytics) Collection API 백 엔드 서버에 대한 성공적인 [세션 요청](../mc-api-ref/mc-api-sessions-req.md)을 완료하는 데 필요한 요청 데이터를 수집합니다. 요청을 수동으로 보내(`curl` 또는 Postman 등을 사용)으로 요청 데이터를 빠르게 확인할 수 있습니다. 이는 요청에 올바르지 않은 데이터 유형 또는 잘못된 정보가 있는지 여부에 대한 즉각적인 피드백을 제공합니다. [JSON 유효성 검사 스키마](../mc-api-ref/mc-api-json-validation.md)을 사용하여 적절한 요청 데이터를 제공했는지 확인합니다.

1. Experience Cloud 애플리케이션을 실행하기 위해 제공해야 하는 표준 필수 Adobe Analytics 및 방문자 데이터를 수집합니다.

   * 방문자 Experience Cloud 조직 ID
   * 방문자 Experience Cloud 사용자 ID
   * Analytics 보고서 세트 ID
   * Analytics 추적 서버 URL

1. 성공적인 호출에 필요한 최소 데이터가 포함된 `sessions` 요청 본문에 대한 JSON 개체를 작성합니다. 예:

   ```json
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
   >JSON 요청 본문에 올바른 데이터 유형을 사용해야 합니다. 예를 들어, `analytics.enableSSL`에는 부울이 필요하고, `media.length`은(는) 숫자입니다. [JSON 유효성 검사 스키마](mc-api-validate-reqs.md)를 확인하여 매개 변수 유형과 필수 및 선택적 요구 사항을 확인할 수 있습니다.

1. MA Collection API 엔드포인트에 세션 요청을 보냅니다. 요청 페이로드가 올바르지 않은 경우 문제를 식별하고 `201 Created` 응답이 나타날 때까지 재시도합니다. 이 `curl` 예제에서 JSON 요청 본문은 `sample_data_session` 파일에 있습니다.

   ```sh
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

위와 유사한 `201 Created` 응답이 [세션 요청](../mc-api-ref/mc-api-sessions-req.md)이 성공하면 나타납니다. 응답에는 위치 헤더에 세션 ID가 포함됩니다. 세션 ID는 모든 후속 추적 호출에 필요하므로 응답의 중요한 정보입니다. 성공적으로 [세션 요청](../mc-api-ref/mc-api-sessions-req.md)을 반환한 후 비디오 플레이어에서 MA API를 사용하여 비디오 추적을 구현하는 작업을 진행할 수 있습니다.
