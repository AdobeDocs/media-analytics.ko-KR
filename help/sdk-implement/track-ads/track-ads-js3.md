---
title: JavaScript 3.x를 사용하여 광고 추적
description: Media SDK를 사용하여 브라우저(JS) 애플리케이션에서 광고 추적을 구현합니다.
translation-type: tm+mt
source-git-commit: f5b3961e0525c26b682490a4376d244c2703ae24
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 80%

---


# JavaScript 3.x를 사용하여 광고 추적{#track-ads-on-javascript}

>[!IMPORTANT]
>
>다음은 3.x SDK를 사용하는 구현과 관련된 지침입니다. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

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

   | 변수 이름 | 유형 | 설명 |
   | --- | --- | --- |
   | `name` | string | adbreak 이름(프리롤, 미드롤 및 포스트롤)을 나타내는 빈 문자열이 아닙니다. |
   | `position` | 수 | 1로 시작하는 광고 브레이크의 번호 위치입니다. |
   | `startTime` | 수 | 광고 브레이크의 시작 위치에 있는 플레이헤드 값입니다. |

   광고 브레이크 개체 작성:

   ```js
   var adBreakObject =
     ADB.Media.createAdBreakObject(<ADBREAK_NAME>,
                                      <POSITION>,
                                      <START_TIME>);
   ```

1. 광고 브레이크 추적을 시작하려면 `MediaHeartbeat` 인스턴스에서 `AdBreakStart`를 사용하여 `trackEvent()`를 호출합니다.

   ```js
   tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);
   ```

1. 광고가 시작되는 시기를 식별하고, 광고 정보를 사용하여 `AdObject` 인스턴스를 만듭니다.

   `AdObject` 참조:

   | 변수 이름 | 유형 | 설명 |
   | --- | --- | --- |
   | `name` | string | 광고 이름을 나타내는 빈 문자열이 아닙니다. |
   | `adId` | string | 광고 식별자를 나타내는 빈 문자열이 아닙니다. |
   | `position` | 수 | 광고 내의 광고 번호 위치(1부터 시작). |
   | `length` | 수 | 광고의 길이를 나타내는 양수. |

   광고 개체 작성:

   ```js
   var adObject =
     ADB.Media.createAdObject.createAdObject(<AD_NAME>,
                                   <AD_ID>,
                                   <POSITION>,
                                   <LENGTH>);
   ```

1. 원할 경우 컨텍스트 데이터 변수를 통해 표준 및/또는 광고 메타데이터를 미디어 추적 세션에 첨부합니다.

   * [JavaScript에서 표준 광고 메타데이터 구현](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-js.md)
   * **사용자 지정 광고 메타데이터 -**&#x200B;사용자 지정 메타데이터의 경우 사용자 지정 데이터 변수에 대한 변수 개체를 만들고, 현재 광고의 데이터로 채웁니다.

      ```js
      /* Set context data */
      // Standard metadata keys provided by adobe.
      adMetadata[ADB.Media.AdMetadataKeys.ADVERTISER]  ="Sample Advertiser";
      adMetadata[ADB.Media.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
      
      // Custom metadata keys
      adMetadata["affiliate"] = "Sample affiliate";
      adMetadata["campaign"] = "Sample ad campaign";
      adMetadata["creative"] = "Sample creative";
      ```

1. 광고 재생 추적을 시작하려면 `MediaHeartbeat` 인스턴스에서 `AdStart` 이벤트를 사용하여 `trackEvent()`를 호출합니다.

   사용자 지정 메타데이터 변수(또는 빈 개체)에 대한 참조를 이벤트 호출의 세 번째 매개 변수로 포함하십시오.

   ```js
   _onAdStart = function() {
       tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
   };
   ```

1. 광고 재생이 광고 끝에 도달하면 `AdComplete` 이벤트를 사용하여 `trackEvent()`를 호출합니다.

   ```js
   _onAdComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdComplete);
   };
   ```

1. 사용자가 광고를 건너뛰도록 선택했기 때문에 광고 재생이 완료되지 않은 경우 `AdSkip` 이벤트를 추적합니다.

   ```js
   _onAdSkip = function() {
       tracker.trackEvent(ADB.Media.Event.AdSkip);
   };
   ```

1. 같은 `AdBreak` 내에 추가 광고가 있는 경우 3~7단계를 다시 반복합니다.
1. 광고 브레이크가 완료되면 `AdBreakComplete` 이벤트를 사용하여 추적합니다.

   ```js
   _onAdBreakComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
   };
   ```

자세한 내용은 추적 시나리오 [프리롤 광고와 함께 VOD 재생](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md)을 참조하십시오.
