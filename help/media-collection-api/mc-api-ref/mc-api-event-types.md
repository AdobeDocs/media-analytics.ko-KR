---
title: 이벤트 유형 및 설명
description: null
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 이벤트 유형 및 설명{#event-types-and-descriptions}

## sessionStart

호출과 함께 `sessions` 전송됩니다. 응답이 반환되면 위치 헤더에서 세션 ID를 추출하여 수집 서버로 후속 이벤트를 호출하는 데 사용합니다.

## play

Sent when the player changes state to "playing" from another state (i.e., the `on('Playing')` callback is triggered by the player). 플레이어가 "재생 중"으로 이동하기 전 상태란 "버퍼링" 상태인 경우, 사용자가 "일시 정지됨" 상태에서 재개한 경우, 플레이어가 오류, 자동 재생 등에서 복구된 경우 등입니다.

## ping

* **기본 컨텐츠 -** 전송된 다른 API 이벤트와 관계없이 기본 컨텐츠 재생 중에 10초마다 전송해야 합니다. 첫 번째 ping 이벤트는 기본 컨텐츠 재생이 시작된 후 10초 후에 발생해야 합니다.
* **광고 컨텐츠 -** 광고 추적 중에 1초마다 전송해야 합니다.

Ping 이벤트는 요청 본문에 *를 포함하지*&#x200B;않아야`params` 합니다.

## bitrateChange

비트레이가 변경되면 전송됩니다.

## bufferStart

버퍼링이 시작될 때 전송됩니다. `bufferResume` 이벤트 유형이 없습니다. A `bufferResume` is inferred when you send a `play` event after `bufferStart`.

## pauseStart

사용자가 일시 중지를 누를 때 전송됩니다. `resume` 이벤트 유형이 없습니다. A `resume` is inferred when you send a `play` event after a `pauseStart`.

## adBreakStart

광고 중단의 시작을 알립니다.

## adStart

광고 시작을 알립니다.

## adComplete

광고 브레이크가 완료되었음을 알립니다.

## adSkip

광고 건너뛰기 알림

## adBreakComplete

광고 브레이크가 완료되었음을 알립니다.

## chapterStart

장 세그먼트의 시작을 알립니다.

## chapterSkip

장 건너뛰기 신호하기

## chapterComplete

장의 완성을 신호함

## 라는 오류가 표시됩니다

오류가 발생했음을 알립니다.

## sessionEnd

이 메서드는 사용자가 컨텐츠 보기를 중단하고 다시 방문할 가능성이 없을 때 세션을 즉시 종료하도록 Media Analytics 백엔드에 알리는 데 사용됩니다.

If you don't send a `sessionEnd`, an abandoned session will time-out normally (after no events are received for 10 minutes, or when no playhead movement occurs for 30 minutes), and the session is deleted by the backend.

## sessionComplete

기본 컨텐츠의 끝에 도달하면 전송됩니다.

>[!IMPORTANT]
>
>You should refer to the [JSON validation schemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) for each event type, to verify correct event parameter types and requirements.

