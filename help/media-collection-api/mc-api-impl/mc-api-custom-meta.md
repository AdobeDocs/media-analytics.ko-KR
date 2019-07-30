---
seo-title: 사용자 지정 메타데이터 지원
title: 사용자 지정 메타데이터 지원
uuid: DF 4109 DD -9 FCA -4 C 33-A 7 D 5-8 E 6 EEC 257527
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 사용자 지정 메타데이터 지원{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. 이 정보는 `customMetadata` 키와 함께 배치된 JSON 키, `params`에 제공해야 합니다.

`customMetadata` JSON 키에는 키 개체가 포함되어야 합니다. 값 쌍을 참조하십시오. 이 키에는 영숫자, 밑줄 및 점/마침표만 사용해야 합니다.

[MA 컬렉션 API 이벤트](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

