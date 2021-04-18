---
title: 사용자 지정 메타데이터 지원
description: 사용자 지정 메타데이터 지원
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 100%

---

# 사용자 지정 메타데이터 지원{#custom-metadata-support}

`sessionStart`, `chapterStart` 및 `adStart` 이벤트에 사용자 지정 키:값 쌍을 제공할 수 있습니다. 이 정보는 `customMetadata` 키와 함께 배치된 JSON 키, `params`에 제공해야 합니다.

키:값 쌍의 개체를 `customMetadata` JSON 키는 포함해야 합니다. 이 키에는 영숫자, 밑줄 및 점/마침표만 사용해야 합니다.

[MA Collection API 이벤트](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)
