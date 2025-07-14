---
title: Chromecast에서 챕터 및 세그먼트를 추적하는 방법에 대해 알아보기
description: Chromecast에서 Media SDK를 사용하여 챕터 및 세그먼트 추적을 구현하는 방법에 대해 알아봅니다.
uuid: 5ea562b9-0e07-4fbb-9a3b-213d746304f5
exl-id: 26b71e4d-ced7-49cb-a838-2b1c8d4ee4de
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 100%

---

# Chromecast에서 챕터 및 세그먼트 추적{#track-chapters-and-segments-on-chromecast}

다음은 2.x SDK를 사용하는 구현과 관련된 지침입니다.

>[!IMPORTANT]
>
> SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/getting-started/download-sdks.md)에서 개발자 안내서를 다운로드할 수 있습니다.

1. 챕터 시작 이벤트가 발생하는 시점을 식별하고, 챕터 정보를 사용하여 `ChapterObject` 인스턴스를 작성합니다.

   `ChapterObject` 챕터 추적 참조:

   >[!NOTE]
   >
   >다음 변수는 챕터를 추적하려는 경우에만 필요합니다.

   | 변수 이름 | 설명 | 필수 여부 |
   | --- | --- | :---: |
   | `name` | 챕터 이름 | 예 |
   | `position` | 챕터 위치 | 예 |
   | `length` | 챕터 길이 | 예 |
   | `startTime` | 챕터 시작 시간 | 예 |

   챕터 개체:[ createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createChapterObject)

   ```js
   chapterInfo = ADBMobile.media.createChapterObject("First Chapter", 1, CHAPTER1_LENGTH, CHAPTER1_START_POS);
   ```

1. 챕터에 대한 사용자 지정 메타데이터를 포함하는 경우 메타데이터에 대한 컨텍스트 데이터 변수를 작성합니다.

   ```js
   var chapterContextData = {
       segmentType: "Sample segment type"
   };
   ```

1. 챕터 재생 추적을 시작하려면 `ChapterStart` 이벤트를 추적합니다([trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)).

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, ChapterInfo, chapterContextData);
   ```

1. 재생이 챕터 종료 경계에 도달하면 사용자 지정 코드에서 정의한 대로 `ChapterComplete` 인스턴스에서 `MediaHeartbeat` 이벤트를 호출합니다([trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)).

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterComplete);
   ```

1. 사용자가 챕터를 건너뛰도록 선택했기 때문에(예: 사용자가 챕터 경계를 찾는 경우) 챕터 재생이 완료되지 않은 경우 `ChapterSkip` 이벤트를 추적합니다([trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)).

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip);
   ```

1. 추가 챕터가 있는 경우 1~5단계를 반복합니다.
