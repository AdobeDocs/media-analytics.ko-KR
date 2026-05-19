---
title: 광고 추적 설명
description: Media SDK를 사용하여 광고 추적을 구현하는 개요입니다.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PguxKIzAL95WbMl5c0yJq9rYSqZgOGbbAYtxOI4eVOs
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 641
ht-degree: 60%

---

# 개요{#overview}

다음은 2.x SDK를 사용하는 구현과 관련된 지침입니다.

>[!IMPORTANT]
>
>SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/getting-started/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

광고 재생에는 추적 광고 브레이크, 광고 시작, 광고 완료 및 광고 건너뛰기가 포함되어 있습니다. 미디어 플레이어의 API를 사용하여 핵심 플레이어 이벤트를 식별하고 필수 및 선택적 광고 변수를 채웁니다.

## 플레이어 이벤트 {#player-events}

### 광고 브레이크 시작 시

>[!NOTE]
>프리롤 포함

* 광고 브레이크에 대한 `adBreak` 개체 인스턴스를 만듭니다. (예: `adBreakObject`)

* 광고 브레이크 시작을 위해 `trackEvent`를 사용하여 `adBreakObject`를 호출합니다.

### 모든 광고 자산 시작 시

* 광고 자산에 대한 광고 개체 인스턴스를 만듭니다. (예: `adObject`)
* 광고 메타데이터, `adCustomMetadata`를 채웁니다.
* 광고 시작을 위해 `trackEvent`를 호출합니다.

### 모든 광고 완료 시

* 광고 완료를 위해 `trackEvent`를 호출합니다.

### 광고를 건너뛸 때

* 광고 건너뛰기를 위해 `trackEvent`를 호출합니다.

### 광고 브레이크 완료 시

* 광고 브레이크 완료를 위해 `trackEvent`를 호출합니다.

## 광고 추적 구현 {#implement-ad-tracking}

### 광고 추적 상수

| 상수 이름 | 설명   |
|---|---|
| `AdBreakStart` | AdBreak 시작 이벤트 추적을 위한 상수 |
| `AdBreakComplete` | AdBreak 완료 이벤트 추적을 위한 상수 |
| `AdStart` | 광고 시작 이벤트 추적을 위한 상수 |
| `AdComplete` | 광고 완료 이벤트 추적을 위한 상수 |
| `AdSkip` | 광고 건너뛰기 이벤트 추적을 위한 상수 |

### 구현 단계

1. 프리롤을 포함하여 광고 브레이크 경계가 시작되는 시점을 식별하고 광고 브레이크 정보를 사용하여 `AdBreakObject`를 생성합니다.

   `AdBreakObject` 참조:

   | 변수 이름 | 설명 | 필수 여부 |
   | --- | --- | :---: |
   | `name` | 프리롤, 미드롤 및 포스트롤 등 광고 브레이크 이름. | 예 |
   | `position` | 콘텐츠 내 광고 브레이크의 번호 위치로서, 1로 시작합니다. | 예 |
   | `startTime` | 광고 브레이크의 시작 위치에 있는 플레이헤드 값입니다. | 예 |

1. 광고 브레이크 추적을 시작하려면 `MediaHeartbeat` 인스턴스에서 `AdBreakStart`를 사용하여 `trackEvent()`를 호출합니다.

1. 광고가 시작되는 시기를 식별하고, 광고 정보를 사용하여 `AdObject` 인스턴스를 만듭니다.

   `AdObject` 참조:

   | 변수 이름 | 설명 | 필수 여부 |
   | --- | --- | :---: |
   | `name` | 친숙한 광고 이름. | 예 |
   | `adId` | 광고에 대한 고유 식별자. | 예 |
   | `position` | 광고 브레이크 내 광고 번호 위치로서 1로 시작합니다. | 예 |
   | `length` | 광고 길이 | 예 |

1. 원할 경우 컨텍스트 데이터 변수를 통해 표준 및/또는 광고 메타데이터를 추적 세션에 첨부합니다.

   * **표준 광고 메타데이터 -** 표준 광고 메타데이터의 경우 플랫폼에 대한 키를 사용하여 표준 광고 메타데이터 키 값 쌍 사전을 만드십시오.
   * **사용자 지정 광고 메타데이터 -** 사용자 지정 메타데이터의 경우 사용자 지정 데이터 변수에 대한 변수 개체를 만들고, 현재 광고의 데이터로 채웁니다.

1. 광고 재생 추적을 시작하려면 `MediaHeartbeat` 인스턴스에서 `AdStart` 이벤트를 사용하여 `trackEvent()`를 호출합니다.

   사용자 지정 메타데이터 변수(또는 빈 개체)에 대한 참조를 이벤트 호출의 세 번째 매개 변수로 포함하십시오. 광고가 재생되는 동안 컨텐츠 플레이헤드(`l:event:playhead`)를 광고 브레이크가 시작된 위치에 고정시켜 두십시오. 광고 재생 시 컨텐츠 재생 시간이 [컨텐츠 체류 시간](/help/reporting/metrics/content-time-spent.md)을 초과합니다.

1. 광고 재생이 광고 끝에 도달하면 `AdComplete` 이벤트를 사용하여 `trackEvent()`를 호출합니다.

1. 사용자가 광고를 건너뛰도록 선택했기 때문에 광고 재생이 완료되지 않은 경우 `AdSkip` 이벤트를 추적합니다.
1. 같은 `AdBreak` 내에 추가 광고가 있는 경우 3~7단계를 다시 반복합니다.
1. 광고 브레이크가 완료되면 `AdBreakComplete` 이벤트를 사용하여 추적합니다.

>[!IMPORTANT]
>
>**프리롤 광고: `AdBreakStart` 및 `AdStart` 전에 `trackPlay`을(를) 호출하지 마십시오.** 기본 콘텐츠의 첫 번째 `play` ping은 [콘텐츠 시작](/help/reporting/metrics/content-starts.md)을 증가시킵니다. 프리롤 광고 이벤트가 실행되기 전에 `trackPlay`이(가) 호출되고 광고 중에 뷰어가 사라지면 기본 콘텐츠가 재생되지 않았더라도 콘텐츠 시작이 증가합니다. 프리롤 시나리오의 경우 `AdBreakStart` 및 `AdStart`이(가) 전송될 때까지 `trackPlay`을(를) 지연합니다.

>[!NOTE]
>
>광고 재생 중에 보고된 플레이헤드 값은 광고 내부가 아닌 **기본 콘텐츠** 내의 뷰어 위치를 나타냅니다. 10분 비디오 앞에 있는 프리롤 광고의 경우 플레이헤드는 전체 광고에서 `0`입니다. 5분 표시에서 시작하는 미드롤 광고의 경우 플레이헤드는 광고 기간 동안 `300`(초)에 유지됩니다.

다음 샘플 코드는 HTML5 미디어 플레이어에 JavaScript 2.x SDK를 사용합니다.

```js
/* Call on ad break start */

if (e.type == "ad break start") {
    var adBreakObject = MediaHeartbeat.createAdBreakObject("mid-roll", 2, 500);
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
};

/* Call on ad start */
if (e.type == "ad start") {
    var adObject = MediaHeartbeat.createAdObject("PepsiOne", "123456ab", 1, 30);
    /* Set custom context data */
    var adCustomMetadata = {
        affiliate:"Sample affiliate",
        campaign:"Sample ad campaign",
        creative:"Sample creative"
    }
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);
};

/* Call on ad complete */
if (e.type == "ad complete") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
};

/* Call on ad skip */
if (e.type == "ad skip") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
};

/* Call on ad break complete */
if (e.type == "ad break complete") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
};
```

>[!MORELIKETHIS]
>
>* [광고 브레이크 시작](/help/implementation/events/ads/ad-break-start.md)
>* [광고 시작](/help/implementation/events/ads/ad-start.md)
>* [광고 완료](/help/implementation/events/ads/ad-complete.md)
>* [광고 건너뛰기](/help/implementation/events/ads/ad-skip.md)
>* [광고 브레이크 완료](/help/implementation/events/ads/ad-break-complete.md)
