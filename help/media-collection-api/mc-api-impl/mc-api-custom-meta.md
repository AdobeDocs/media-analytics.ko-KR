---
title: 사용자 지정 메타데이터 지원
description: null
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 사용자 지정 메타데이터 지원{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. 이 정보는 `customMetadata` 키와 함께 배치된 JSON 키, `params`에 제공해야 합니다.

The `customMetadata` JSON key should contain an object of key:value pairs. 이 키에는 영숫자, 밑줄 및 점/마침표만 사용해야 합니다.

[MA 컬렉션 API 이벤트](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

