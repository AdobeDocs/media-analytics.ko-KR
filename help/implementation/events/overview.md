---
title: 스트리밍 미디어 이벤트 개요
description: 미디어 이벤트 유형 및 전송 순서에 대해 알아봅니다.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 4%

---


# 스트리밍 미디어 이벤트

스트리밍 미디어 추적은 플레이어 상태 전환을 나타내는 이벤트 호출 시퀀스를 Adobe 데이터 수집 끝점으로 보내어 작동합니다. 모든 이벤트는 [sessionStart](session/session-start.md) 호출로 시작하고 [sessionComplete](session/session-complete.md) 또는 [sessionEnd](session/session-end.md)(으)로 끝나는 활성 세션에 속합니다.

## 이벤트 워크플로

다음의 순서가 지정된 목록은 프리롤 광고와 한 개의 챕터가 있는 일반적인 VOD 재생에 대한 필수 이벤트 시퀀스를 보여 줍니다.

1. **[세션 시작](session/session-start.md)**: 항상 첫 번째 이벤트입니다. 세션을 만들고 세션 ID를 반환합니다.
2. **[광고 브레이크 시작](ads/ad-break-start.md)**: 광고 이벤트보다 먼저 필요합니다.
3. **[광고 시작](ads/ad-start.md)** → **[광고 완료](ads/ad-complete.md)**(또는 **[광고 건너뛰기](ads/ad-skip.md)**)
4. **[광고 브레이크 완료](ads/ad-break-complete.md)**: 브레이크에 있는 모든 광고 다음에 필요합니다.
5. **[재생](playback/play.md)**: 콘텐츠 재생이 시작되거나 다시 시작됨을 알립니다.
6. **[챕터 시작](chapters/chapter-start.md)**: 선택 사항입니다. 챕터의 시작을 표시합니다.
7. **[Ping](playback/ping.md)**: 기본 콘텐츠 중에 10초마다, 광고 중에 1초마다 전송됩니다.
8. **[챕터 완료](chapters/chapter-complete.md)**: 선택 사항입니다. 챕터의 끝을 표시합니다
9. **[일시 중지 시작](playback/pause-start.md)** → **[재생](playback/play.md)**(다시 시작): 일시 중지
10. **[버퍼 시작](playback/buffer-start.md)** → **[재생](playback/play.md)**(다시 시작): 모든 버퍼링의 경우
11. **[세션 완료](session/session-complete.md)**: 뷰어가 콘텐츠의 끝에 도달할 때

뷰어가 콘텐츠의 끝에 도달하기 전에 세션을 중단하는 경우 세션 완료 대신 [세션 종료](session/session-end.md)를 사용하십시오.

## 세션 라이프사이클

다음 조건 중 하나가 충족되면 세션이 자동으로 만료됩니다.

* **10분** 동안 받은 이벤트가 없습니다.
* **30분** 동안 플레이헤드 이동 없음

## 이벤트 참조

| 이벤트 | 카테고리 | 관련 지표 |
| --- | --- | --- |
| [세션 시작](session/session-start.md) | 세션 | [미디어 시작](/help/reporting/metrics/media-starts.md) |
| [세션 완료](session/session-complete.md) | 세션 | [컨텐츠 완료](/help/reporting/metrics/content-completes.md) |
| [세션 종료](session/session-end.md) | 세션 | — |
| [재생](playback/play.md) | 재생 | [콘텐츠 시작](/help/reporting/metrics/content-starts.md) |
| [시작 일시 중지](playback/pause-start.md) | 재생 | [이벤트 일시 중지](/help/reporting/metrics/pause-events.md) |
| [버퍼 시작](playback/buffer-start.md) | 재생 | [버퍼 이벤트](/help/reporting/metrics/buffer-events.md) |
| [비트율 변경](playback/bitrate-change.md) | 재생 | [비트율 변경](/help/reporting/metrics/bitrate-changes.md) |
| [Ping](playback/ping.md) | 재생 | — |
| [광고 브레이크 시작](ads/ad-break-start.md) | 광고 | — |
| [광고 시작](ads/ad-start.md) | 광고 | [광고 시작](/help/reporting/metrics/ad-starts.md) |
| [광고 완료](ads/ad-complete.md) | 광고 | [광고 완료](/help/reporting/metrics/ad-completes.md) |
| [광고 건너뛰기](ads/ad-skip.md) | 광고 | — |
| [광고 브레이크 완료](ads/ad-break-complete.md) | 광고 | — |
| [챕터 시작](chapters/chapter-start.md) | 챕터 | [챕터 시작](/help/reporting/metrics/chapter-starts.md) |
| [챕터 완료](chapters/chapter-complete.md) | 챕터 | [챕터 완료](/help/reporting/metrics/chapter-completes.md) |
| [챕터 건너뛰기](chapters/chapter-skip.md) | 챕터 | — |
| [상태 시작](player-state/state-start.md) | 플레이어 상태 | 주마다 다름 |
| [상태 끝](player-state/state-end.md) | 플레이어 상태 | 주마다 다름 |
| [오류](error.md) | 품질 | [오류 영향을 받은 스트림](/help/reporting/metrics/error-impacted-streams.md) |

>[!MORELIKETHIS]
>
>* [JSON 유효성 검사 스키마](/help/implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md): 각 이벤트 유형에 대한 요청 페이로드 구조를 확인하십시오.
>* [이벤트 요청 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md): Media Collection API 끝점 참조
>* [세션 요청 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md): 이벤트를 보내기 전에 세션을 만듭니다.
>* [플레이어 상태 추적](/help/use-cases/player-state-tracking/implementation-and-reporting.md): 상태 시작 및 상태 종료 구현 세부 정보
