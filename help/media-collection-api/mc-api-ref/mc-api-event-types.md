---
title: 이벤트 유형 및 설명
description: null
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 이벤트 유형 및 설명{#event-types-and-descriptions}

## sessionStart

`sessions` 호출을 사용하여 전송됩니다. 응답이 반환되면 위치 헤더에서 세션 ID를 추출하여 수집 서버로 후속 이벤트를 호출하는 데 사용합니다.

## play

플레이어가 다른 상태에서 &quot;재생 중&quot; 상태로 변경되면(예: `on('Playing')` 콜백이 플레이어에 의해 트리거됨) 전송됩니다. 플레이어가 &quot;재생 중&quot;으로 이동하기 전 상태란 &quot;버퍼링&quot; 상태인 경우, 사용자가 &quot;일시 정지됨&quot; 상태에서 재개한 경우, 플레이어가 오류, 자동 재생 등에서 복구된 경우 등입니다.

## ping

* **기본 컨텐츠 -** 전송된 다른 API 이벤트와 관계없이 기본 컨텐츠 재생 중에 10초마다 전송해야 합니다. 첫 번째 핑 이벤트는 기본 컨텐츠 재생이 시작되고 10초 후에 발생합니다.
* **광고 컨텐츠 -** 광고 추적 중에 1초마다 전송해야 합니다.

Ping 이벤트는 요청 본문에 *를 포함하지*&#x200B;않아야`params` 합니다.

## bitrateChange

비트 전송률이 변경되면 전송됩니다.

## bufferStart

버퍼링이 시작되면 전송됩니다. `bufferResume` 이벤트 유형이 없습니다. `bufferResume`은 `play` 이벤트를 `bufferStart` 다음에 보낼 때 추론됩니다.

## pauseStart

사용자가 일시 정지를 누르면 전송됩니다. `resume` 이벤트 유형이 없습니다. `resume`은 `play` 이벤트를 `pauseStart` 다음에 보낼 때 추론됩니다.

## adBreakStart

광고 브레이크를 시작한다는 신호를 보냅니다.

## adStart

광고를 시작한다는 신호를 보냅니다.

## adComplete

광고 브레이크를 완료한다는 신호를 보냅니다.

## adSkip

광고를 건너뛴다는 신호를 보냅니다.

## adBreakComplete

광고 브레이크를 완료한다는 신호를 보냅니다.

## chapterStart

챕터 세그먼트를 시작한다는 신호를 보냅니다.

## chapterSkip

챕터를 건너뛴다는 신호를 보냅니다.

## chapterComplete

챕터를 종료한다는 신호를 보냅니다.

## 라는 오류가 표시됩니다

오류가 발생했다는 신호를 보냅니다.

## sessionEnd

사용자가 컨텐츠 보기를 중단한 경우 세션을 즉시 닫도록 Media Analytics 백 엔드에 통지하는 데 사용되며, 반환 가능성이 낮습니다.

중단된 세션이 `sessionEnd`를 보내지 않는 경우 시간 초과되어(10분 동안 이벤트가 수신되지 않았거나 30분 동안 플레이헤드 이동이 발생하지 않은 경우) 백 엔드에서 해당 세션이 삭제됩니다.

## sessionComplete

기본 컨텐츠의 끝에 도달했을 때 전송됩니다.

>[!IMPORTANT]
>
>각 이벤트 유형에 대한 [JSON 유효성 검사 스키마](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)를 참조하여 올바른 이벤트 매개 변수 유형 및 요구 사항을 확인해야 합니다.

