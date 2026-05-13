---
title: 테스트 2 미디어 중단
description: 유효성 검사에 사용되는 미디어 중단 테스트에 대해 알아봅니다.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/gVEDMjM05nDnzCB6l-9CjyUzoArcmyN4jgsjmjllRiY
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 248
ht-degree: 100%

---

# 테스트 2: 미디어 중단{#test-media-interruption}

이 테스트 케이스는 모바일 중단 동작의 유효성을 검사합니다.

## 테스트 절차

다음 순서로 이 작업을 완료하고 기록해야 합니다.

1. **미디어 플레이어 시작**

   미디어 플레이어가 시작되면 다음 호출이 다음 순서로 전송됩니다.

   1. Adobe Analytics(AppMeasurement) 시작
   1. Media Analytics(하트비트) 시작
   1. Media Analytics(하트비트) Adobe Analytics 시작 호출 요청

   위의 처음 두 호출에는 추가 메타데이터와 변수가 포함되어 있습니다. 호출 매개 변수 및 메타데이터에 대해서는 [테스트 호출 세부 사항](/help/legacy/validation/test-call-details.md#start-the-media-player)을 참조하십시오.

   위에서 세 번째 호출은 Media SDK가 Adobe Analytics 시작 호출(`pev2=ms_s`)을 Adobe Analytics 서버로 전송하도록 요청했음을 Media Analytics 서버에 알려줍니다.

1. **적어도 5분 동안 중단되지 않은 상태로 기본 콘텐츠 재생**

   **콘텐츠 재생**

   콘텐츠를 재생하는 동안 Media SDK는 10초마다 재생 호출(하트비트)을 Media Analytics 서버로 전송합니다.

   호출 매개 변수 및 메타데이터에 대해서는 [테스트 호출 세부 사항](/help/legacy/validation/test-call-details.md#play-main-content)을 참조하십시오.

   이러한 광고 호출에 대한 추가 정보가 필요하면 플랫폼의 [광고 추적](/help/use-cases/track-ads/track-ads-overview.md) 지침을 참조하십시오.

1. **앱 또는 브라우저를 백그라운드로 이동**

   앱이 백그라운드에서 실행되는 동안 `main:pause` 호출만 VHL 버전 1.6.6 이상으로 시작되는 Media Analytics 서버로 전송되어야 합니다.

1. **앱 또는 브라우저를 전경으로 다시 가져오기**

   백그라운드에서 돌아올 때 콘텐츠 재생이 재개되어야 합니다.

1. **적어도 5분 동안 중단되지 않은 상태로 기본 콘텐츠 미디어 재생**

   호출 매개 변수 및 메타데이터에 대해서는 [테스트 호출 세부 사항](/help/legacy/validation/test-call-details.md#play-main-content)을 참조하십시오.

1. **미디어 플레이어 닫기**

   미디어 플레이어를 닫으면 추가 추적 통화가 발생하지 않습니다.
