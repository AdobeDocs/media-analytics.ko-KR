---
title: JavaScript 3.x를 사용하여 장 및 세그먼트 추적
description: 이 항목에서는 브라우저 앱(JS)에서 Media SDK를 사용하여 챕터 및 세그먼트 추적을 구현하는 방법에 대해 설명합니다.
translation-type: tm+mt
source-git-commit: b14b56aea4a1821a2a160b9cd301cd181f1ba8dd
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 71%

---


# JavaScript 3.x를 사용하여 장 및 세그먼트 추적{#track-chapters-and-segments-on-javascript}

>[!IMPORTANT]
>
>다음은 3.x SDK를 사용하는 구현과 관련된 지침입니다. If you are implementing any previous versions of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

1. 챕터 시작 이벤트가 발생하는 시점을 식별하고, 챕터 정보를 사용하여 `ChapterObject` 인스턴스를 작성합니다.

   `ChapterObject` 챕터 추적 참조:

   >[!NOTE]
   >
   >다음 변수는 챕터를 추적하려는 경우에만 필요합니다.

   | 변수 이름 | 유형 | 설명 |
   | --- | --- | --- |
   | `name` | string | 장 이름을 나타내는 빈 문자열이 아닙니다. |
   | `position` | 수 | 컨텐츠 내의 장(1부터 시작)의 위치입니다. |
   | `length` | 수 | 장의 길이를 나타내는 양수. |
   | `startTime` | 수 | 장 시작 시 재생 헤드 값. |

   챕터 개체:

   ```js
   var chapterObject =
     ADB.Media.createChapterObject.createChapterObject(<CHAPTER_NAME>,
                                        <POSITION>,
                                        <LENGTH>,
                                        <START_TIME>);
   ```

1. 챕터에 대한 사용자 지정 메타데이터를 포함하는 경우 메타데이터에 대한 컨텍스트 데이터 변수를 작성합니다.

   ```js
   var chapterMetadata = {};
   chapterMetadata["segmentType"] = "Sample segment type";
   ```

1. 챕터 재생 추적을 시작하려면 `ChapterStart` 인스턴스에서 `MediaHeartbeat` 이벤트를 호출합니다.

   ```js
   _onChapterStart = function() {
     tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);
   
   };
   ```

1. 재생이 챕터 종료 경계에 도달하면 사용자 지정 코드에서 정의한 대로 인스턴스에서 `ChapterComplete` 이벤트를 호출합니다:`MediaHeartbeat`

   ```js
   _onChapterComplete = function() {
      tracker.trackEvent(ADB.Media.Event.ChapterComplete);
   };
   ```

1. 사용자가 챕터를 건너뛰도록 선택했기 때문에(예: 사용자가 챕터 경계를 찾는 경우) 챕터 재생이 완료되지 않은 경우 MediaHeartbeat 인스턴스에서 `ChapterSkip` 이벤트를 호출합니다:

   ```js
   _onChapterSkip = function() {
       tracker.trackEvent(ADB.Media.Event.ChapterSkip);
   };
   ```

1. 추가 챕터가 있는 경우 1~5단계를 반복합니다.
