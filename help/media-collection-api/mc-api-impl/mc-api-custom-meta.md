---
title: 사용자 지정 메타데이터 지원
description: '"sessionStart, chapterStart 및 adStart 이벤트에 사용자 지정 키:값 쌍을 제공하는 방법을 알아봅니다."'
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 48%

---

# 사용자 지정 메타데이터 지원{#custom-metadata-support}

`sessionStart`, `chapterStart` 및 `adStart` 이벤트에 사용자 지정 키:값 쌍을 제공할 수 있습니다. 이 정보는 `customMetadata` 키와 함께 배치된 JSON 키, `params`에 제공해야 합니다.

키:값 쌍의 개체를 `customMetadata` JSON 키는 포함해야 합니다. 이 키에는 영숫자, 밑줄 및 점/마침표만 사용해야 합니다.

[MA Collection API 이벤트](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

## 예

현재 키:값 쌍으로 `sessionStart` 이벤트를 보낼 수 있습니다.

```
params: { "media.channel": "channel-1" },
  customMetadata: { "a.media.channel": "channel-2" }
```

위의 구성에 대해 analytics에 전송된 보고 데이터는 다음과 같습니다.

`c.a.media.channel=channel-2`

### 권장 사항

사용자 지정 메타데이터에 별도의 네임스페이스를 사용하는 것이 좋습니다. 예를 들어,

```
params: { "media.channel": "channel-1" },
  customMetadata: { "clientnamespace.media.channel": "channel-2" }
```

권장되는 예에서 analytics로 전송된 사용자 지정 메타데이터에 대한 보고 데이터는 다음과 같습니다.

`c.a.media.channel=channel-1`
`c.clientnamespace.media.channel=channel-2`
