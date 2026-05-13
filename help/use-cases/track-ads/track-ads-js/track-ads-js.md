---
title: JavaScript 2.x를 사용하여 광고를 추적하는 방법에 대해 알아보기
description: Media SDK를 사용하여 브라우저(JS) 애플리케이션에서 광고 추적을 구현합니다.
uuid: 4d81d29c-c55d-4d48-b505-3260922712ff
exl-id: 4404d3a6-ab98-40f0-9573-ee32f480f650
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/ItWdBdCHpR9E0OiZNKTNaPs-3cWWrdWouHn6TP9-RWA
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 369
ht-degree: 91%

---

# JavaScript 2.x를 사용하여 광고 추적{#track-ads-on-javascript}

다음은 2.x SDK를 사용하는 구현과 관련된 지침입니다.

>[!IMPORTANT]
>
>SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/getting-started/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

## 광고 추적 상수

| 상수 이름 | 설명   |
|---|---|
| `AdBreakStart` | AdBreak 시작 이벤트 추적을 위한 상수 |
| `AdBreakComplete` | AdBreak 완료 이벤트 추적을 위한 상수 |
| `AdStart` | 광고 시작 이벤트 추적을 위한 상수 |
| `AdComplete` | 광고 완료 이벤트 추적을 위한 상수 |
| `AdSkip` | 광고 건너뛰기 이벤트 추적을 위한 상수 |

## 구현 단계

1. 프리롤을 포함하여 광고 브레이크 경계가 시작되는 시점을 식별하고 광고 브레이크 정보를 사용하여 `AdBreakObject`를 생성합니다.

   `AdBreakObject` 참조:

   | 변수 이름 | 설명 | 필수 여부 |
   | --- | --- | :---: |
   | `name` | 프리롤, 미드롤 및 포스트롤 등 광고 브레이크 이름. | 예 |
   | `position` | 1로 시작하는 광고 브레이크의 번호 위치입니다. | 예 |
   | `startTime` | 광고 브레이크의 시작 위치에 있는 플레이헤드 값입니다. | 예 |

   광고 브레이크 개체 작성:

   ```js
   var adBreakObject =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. 광고 브레이크 추적을 시작하려면 `MediaHeartbeat` 인스턴스에서 `AdBreakStart`를 사용하여 `trackEvent()`를 호출합니다.

   ```js
   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
   ```

1. 광고가 시작되는 시기를 식별하고, 광고 정보를 사용하여 `AdObject` 인스턴스를 만듭니다.

   `AdObject` 참조:

   | 변수 이름 | 설명 | 필수 여부 |
   | --- | --- | :---: |
   | `name` | 친숙한 광고 이름. | 예 |
   | `adId` | 광고에 대한 고유 식별자. | 예 |
   | `position` | 광고 브레이크 내 광고 번호 위치로서 1로 시작합니다. | 예 |
   | `length` | 광고 길이 | 예 |

   광고 개체 작성:

   ```js
   var adObject =  
     MediaHeartbeat.createAdObject(<AD_NAME>,  
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. 원할 경우 컨텍스트 데이터 변수를 통해 표준 및/또는 광고 메타데이터를 미디어 추적 세션에 첨부합니다.

   * [JavaScript에서 표준 광고 메타데이터 구현](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
   * **사용자 지정 광고 메타데이터 -**&#x200B;사용자 지정 메타데이터의 경우 사용자 지정 데이터 변수에 대한 변수 개체를 만들고, 현재 광고의 데이터로 채웁니다.

     ```js
     /* Set custom context data */
     var adCustomMetadata = {
         affiliate: "Sample affiliate",
         campaign: "Sample ad campaign",
         creative: "Sample creative"
     };
     ```

1. 광고 재생 추적을 시작하려면 `MediaHeartbeat` 인스턴스에서 `AdStart` 이벤트를 사용하여 `trackEvent()`를 호출합니다.

   사용자 지정 메타데이터 변수(또는 빈 개체)에 대한 참조를 이벤트 호출의 세 번째 매개 변수로 포함하십시오.

   ```js
   _onAdStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                                       adObject,  
                                       adCustomMetadata);
   };
   ```

1. 광고 재생이 광고 끝에 도달하면 `AdComplete` 이벤트를 사용하여 `trackEvent()`를 호출합니다.

   ```js
   _onAdComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
   };
   ```

1. 사용자가 광고를 건너뛰도록 선택했기 때문에 광고 재생이 완료되지 않은 경우 `AdSkip` 이벤트를 추적합니다.

   ```js
   _onAdSkip = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
   };
   ```

1. 같은 `AdBreak` 내에 추가 광고가 있는 경우 3~7단계를 다시 반복합니다.
1. 광고 브레이크가 완료되면 `AdBreakComplete` 이벤트를 사용하여 추적합니다.

   ```js
   _onAdBreakComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
   };
   ```

자세한 내용은 추적 시나리오 [프리롤 광고와 함께 VOD 재생](/help/use-cases/tracking-scenarios/vod-preroll-ads.md)을 참조하십시오.
