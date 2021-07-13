---
title: 장 및 세그먼트를 추적하는 방법 알아보기
description: Media SDK를 사용하여 챕터 및 세그먼트 추적을 구현하는 방법입니다.
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 97%

---

# 개요{#overview}

>[!IMPORTANT]
>
>다음은 2.x SDK를 사용하는 구현과 관련된 지침입니다. SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/sdk-implement/download-sdks.md)에서 개발자 안내서를 다운로드할 수 있습니다.

챕터 및 세그먼트 추적은 사용자 지정 미디어 챕터 또는 세그먼트에 사용할 수 있습니다. 일부는 챕터 추적에 사용되며, 야구 이닝과 같은 미디어 컨텐츠를 기반으로 하여 사용자 지정 세그먼트를 정의하거나 광고 브레이크 간의 컨텐츠 세그먼트를 정의합니다. 챕터 추적은 코어 미디어 추적 구현에 필요하지 **않습니다**.

챕터 추적에는 챕터 시작, 챕터 완료, 챕터 건너뛰기가 포함됩니다. 사용자 지정된 세그멘테이션 논리에 미디어 플레이어 API를 사용하여 챕터 이벤트를 식별하고 필수 및 선택적 챕터 변수를 채울 수 있습니다.

## 플레이어 이벤트

### 챕터 시작 시

* 챕터 `chapterObject`에 대한 챕터 개체 인스턴스 작성
* 챕터 메타데이터, `chapterCustomMetadata`채우기
* 호출 `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### 챕터 완료 시

* 호출 `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### 챕터를 건너뛸 때

* 호출 `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## 챕터 추적 구현 {#implement-chapter-tracking}

1. 챕터 시작 이벤트가 발생하는 시점을 식별하고, 챕터 정보를 사용하여 `ChapterObject` 인스턴스를 작성합니다.

   다음은 `ChapterObject` 챕터 추적 참조입니다.

   >[!NOTE]
   >
   >다음 변수는 챕터를 추적하려는 경우에만 필요합니다.

   | 변수 이름 | 설명 | 필수 여부 |
   | --- | --- | :---: |
   | `name` | 챕터 이름 | 예 |
   | `position` | 챕터 위치 | 예 |
   | `length` | 챕터 길이 | 예 |
   | `startTime` | 챕터 시작 시간 | 예 |

1. 챕터에 대한 사용자 지정 메타데이터를 포함하는 경우 메타데이터에 대한 컨텍스트 데이터 변수를 작성합니다.
1. 챕터 재생 추적을 시작하려면 `ChapterStart` 인스턴스에서 `MediaHeartbeat` 이벤트를 호출합니다.
1. 재생이 챕터 종료 경계에 도달하면 사용자 지정 코드에서 정의한 대로 인스턴스에서 `ChapterComplete` 이벤트를 호출합니다.`MediaHeartbeat`
1. 사용자가 챕터를 건너뛰도록 선택했기 때문에(예: 사용자가 챕터 경계를 찾는 경우) 챕터 재생이 완료되지 않은 경우 MediaHeartbeat 인스턴스에서 `ChapterSkip` 이벤트를 호출합니다.
1. 추가 챕터가 있는 경우 1~5단계를 반복합니다.

다음 샘플 코드는 HTML5 미디어 플레이어에 JavaScript 2.x SDK를 사용합니다. 이 코드는 코어 미디어 재생 코드와 함께 사용해야 합니다.

```js
/* Call on chapter start */ 
if (e.type == "chapter start") { 
    var chapterObject = MediaHeartbeat.createChapterObject("Inning 5",5,500,2500); 
    /* Set custom context data*/ 
    var chapterCustomMetadata = { 
        segmentType:"Baseball Innings", 
        segmentName:"Inning 5", 
        segmentInfo:"Game Six" 
    } 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                   chapterObject,  
                                   chapterCustomMetadata); 
}; 
 
/* Call on chapter complete */ 
if (e.type == "chapter complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
}; 
 
/* Call on chapter skip */ 
if (e.type == "chapter skip") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
}; 
```
