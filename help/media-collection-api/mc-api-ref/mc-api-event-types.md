---
seo-title: 이벤트 유형 및 설명
title: 이벤트 유형 및 설명
uuid: bc 4 f 75 a 7-ea 22-47 eb-a 50 d -5 f 41274 c 6 d 41
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 이벤트 유형 및 설명{#event-types-and-descriptions}

## sessionStart

Sent with the `sessions` call. 응답이 반환되면 위치 헤더에서 세션 ID를 추출하여 수집 서버로 후속 이벤트를 호출하는 데 사용합니다.

## play

Sent when the player changes state to "playing" from another state (i.e., the `on('Playing')` callback is triggered by the player). 플레이어가 "재생 중"으로 이동하기 전 상태란 "버퍼링" 상태인 경우, 사용자가 "일시 정지됨" 상태에서 재개한 경우, 플레이어가 오류, 자동 재생 등에서 복구된 경우 등입니다.

## ping

* **기본 컨텐츠 -** 전송된 다른 API 이벤트와 관계없이 기본 컨텐츠 재생 중에 10초마다 전송해야 합니다. 첫 번째 ping 이벤트는 기본 컨텐츠 재생이 시작된 후 10초 후에 발생해야 합니다.
* **광고 컨텐츠 -** 광고 추적 중에 1초마다 전송해야 합니다.

Ping 이벤트는 요청 본문에 *를 포함하지*&#x200B;않아야`params` 합니다.

## Bitratechange

bitrage 변경 시 전송됩니다.

## bufferStart

버퍼링이 시작될 때 전송됩니다. `bufferResume` 이벤트 유형이 없습니다. A `bufferResume` is inferred when you send a `play` event after `bufferStart`.

## pauseStart

사용자가 일시 중지를 누를 때 전송됩니다. `resume` 이벤트 유형이 없습니다. A `resume` is inferred when you send a `play` event after a `pauseStart`.

## adBreakStart

광고 브레이크 시작 신호

## adStart

광고 시작을 알립니다.

## adComplete

광고 브레이크 완료 신호

## adSkip

광고 생략 신호

## adBreakComplete

광고 브레이크 완료 신호

## chapterStart

챕터 세그먼트의 시작을 알립니다.

## chapterSkip

챕터 건너뛰기 신호

## chapterComplete

챕터 완료 신호

## 라는 오류가 표시됩니다

오류가 발생했음을 알립니다.

## sessionEnd

사용자가 콘텐트 보기를 포기했고 다시 돌아갈 가능성은 없을 때 미디어 분석 백엔드를 알리는 데 사용됩니다.

If you don't send a `sessionEnd`, an abandoned session will time-out normally (after no events are received for 10 minutes, or when no playhead movement occurs for 30 minutes), and the session is deleted by the backend.

## sessionComplete

주 컨텐츠 끝에 도달하면 전송됩니다.

>[!IMPORTANT]
>
>You should refer to the [JSON validation schemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) for each event type, to verify correct event parameter types and requirements.

