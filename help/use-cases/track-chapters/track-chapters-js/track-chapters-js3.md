---
title: JavaScript 3.x를 사용하여 챕터 및 세그먼트를 추적하는 방법에 대해 알아보기
description: 브라우저 앱(JS)에서 Media SDK를 사용하여 챕터 및 세그먼트 추적을 구현하는 방법에 대해 알아봅니다.
exl-id: 00ba11df-d226-45a2-a561-dc9f15dcf714
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 100%

---

# JavaScript 3.x를 사용하여 챕터 및 세그먼트 추적{#track-chapters-and-segments-on-javascript}

다음은 3.x SDK를 사용하는 구현과 관련된 지침입니다.

>[!IMPORTANT]
>
> SDK의 이전 버전을 구현하는 경우, [SDK 다운로드](/help/getting-started/download-sdks.md)에서 개발자 안내서를 다운로드할 수 있습니다.

1. 챕터 시작 이벤트가 발생하는 시점을 식별하고, 챕터 정보를 사용하여 `ChapterObject` 인스턴스를 작성합니다.

   `ChapterObject` 챕터 추적 참조:

   >[!NOTE]
   >
   >다음 변수는 챕터를 추적하려는 경우에만 필요합니다.

   | 변수 이름 | 유형 | 설명 |
   | --- | --- | --- |
   | `name` | 문자열 | 챕터 이름을 나타내는 빈 문자열이 아닙니다. |
   | `position` | 숫자 | 콘텐츠 내 챕터 위치로서, 1로 시작합니다. |
   | `length` | 숫자 | 챕터 길이를 나타내는 양수입니다. |
   | `startTime` | 숫자 | 챕터 시작 위치에 있는 플레이헤드 값입니다. |

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

1. 재생이 챕터 종료 경계에 도달하면 사용자 지정 코드에서 정의한 대로 인스턴스에서 `ChapterComplete` 이벤트를 호출합니다.`MediaHeartbeat`

   ```js
   _onChapterComplete = function() {
      tracker.trackEvent(ADB.Media.Event.ChapterComplete);
   };
   ```

1. 사용자가 챕터를 건너뛰도록 선택했기 때문에(예: 사용자가 챕터 경계를 찾는 경우) 챕터 재생이 완료되지 않은 경우 MediaHeartbeat 인스턴스에서 `ChapterSkip` 이벤트를 호출합니다.

   ```js
   _onChapterSkip = function() {
       tracker.trackEvent(ADB.Media.Event.ChapterSkip);
   };
   ```

1. 추가 챕터가 있는 경우 1~5단계를 반복합니다.
