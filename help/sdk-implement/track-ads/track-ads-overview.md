---
title: 광고 추적 설명
description: Media SDK를 사용하여 광고 추적을 구현하는 개요입니다.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 99%

---

# 개요{#overview}

>[!IMPORTANT]
>
>다음은 2.x SDK를 사용하는 구현과 관련된 지침입니다. SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/sdk-implement/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

광고 재생에는 추적 광고 브레이크, 광고 시작, 광고 완료 및 광고 건너뛰기가 포함되어 있습니다. 미디어 플레이어의 API를 사용하여 핵심 플레이어 이벤트를 식별하고 필수 및 선택적 광고 변수를 채웁니다. 포괄적인 메타데이터 목록은 [광고 매개 변수](/help/metrics-and-metadata/ad-parameters.md)를 참조하십시오.

## 플레이어 이벤트 {#player-events}


### 광고 브레이크 시작 시

>[!NOTE]
>프리롤 포함

* 광고 브레이크에 대한 `adBreak` 개체 인스턴스를 만듭니다. 예, `adBreakObject`.

* 광고 브레이크 시작을 위해 `trackEvent`를 사용하여 `adBreakObject`를 호출합니다.

### 모든 광고 자산 시작 시

* 광고 자산에 대한 광고 개체 인스턴스를 만듭니다. 예, `adObject`.
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
   | `name` | 프리롤, 미드롤 및 포스트롤과 같은 광고 브레이크 이름입니다. | 예 |
   | `position` | 컨텐츠 내 광고 브레이크의 번호 위치로서, 1로 시작합니다. | 예 |
   | `startTime` | 광고 브레이크의 시작 위치에 있는 플레이헤드 값입니다. | 예 |

1. 광고 브레이크 추적을 시작하려면 `MediaHeartbeat` 인스턴스에서 `AdBreakStart`를 사용하여 `trackEvent()`를 호출합니다.

1. 광고가 시작되는 시기를 식별하고, 광고 정보를 사용하여 `AdObject` 인스턴스를 만듭니다.

   `AdObject` 참조:

   | 변수 이름 | 설명 | 필수 여부 |
   | --- | --- | :---: |
   | `name` | 친숙한 광고 이름. | 예 |
   | `adId` | 광고의 고유 식별자. | 예 |
   | `position` | 광고 브레이크 내 광고 번호 위치로서, 1로 시작합니다. | 예 |
   | `length` | 광고 길이 | 예 |

1. 원할 경우 컨텍스트 데이터 변수를 통해 표준 및/또는 광고 메타데이터를 추적 세션에 첨부합니다.

   * **표준 광고 메타데이터 -** 표준 광고 메타데이터의 경우, 플랫폼에 대한 키를 사용하여 표준 광고 메타데이터 키 값 쌍 사전을 만드십시오.
   * **사용자 지정 광고 메타데이터 -**&#x200B;사용자 지정 메타데이터의 경우 사용자 지정 데이터 변수에 대한 변수 개체를 만들고, 현재 광고의 데이터로 채웁니다.

1. 광고 재생 추적을 시작하려면 `MediaHeartbeat` 인스턴스에서 `AdStart` 이벤트를 사용하여 `trackEvent()`를 호출합니다.

   사용자 지정 메타데이터 변수(또는 빈 개체)에 대한 참조를 이벤트 호출의 세 번째 매개 변수로 포함하십시오.

1. 광고 재생이 광고 끝에 도달하면 `AdComplete` 이벤트를 사용하여 `trackEvent()`를 호출합니다.

1. 사용자가 광고를 건너뛰도록 선택했기 때문에 광고 재생이 완료되지 않은 경우 `AdSkip` 이벤트를 추적합니다.
1. 같은 `AdBreak` 내에 추가 광고가 있는 경우 3~7단계를 다시 반복합니다.
1. 광고 브레이크가 완료되면 `AdBreakComplete` 이벤트를 사용하여 추적합니다.

>[!IMPORTANT]
>
>광고 재생(`s:asset:type=ad`) 중에 컨텐츠 플레이어 플레이헤드(`l:event:playhead`)를 증가시키지 않도록 하십시오. 증가시킬 경우 컨텐츠 체류 시간 지표가 부정적인 영향을 받습니다.

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
