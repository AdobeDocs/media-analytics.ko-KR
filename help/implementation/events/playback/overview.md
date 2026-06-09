---
title: 재생 추적
description: 재생 이벤트와 재생, 일시 중지, 버퍼, Ping 및 비트율 변경 추적을 구현하는 방법에 대해 알아봅니다.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Cc5T13Z1S15MyG-CxpxMoHX-ckULmIe0dfUOe7650DE
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 231
ht-degree: 2%

---


# 재생 추적

재생 이벤트는 세션 전체에서 미디어 플레이어에서 상태 전환을 추적합니다. 이벤트 스트림의 코어를 형성하고 모든 콘텐츠 유형에 적용됩니다.

## 플레이어 이벤트

| 플레이어 이벤트 | 액션 |
| --- | --- |
| 미디어 재생 또는 다시 시작 | 통화 재생 |
| 미디어 일시 중지 | 호출 일시 중지 시작 |
| 버퍼링 시작 | 호출 버퍼 시작 |
| 버퍼링 종료 | 통화 재생 |
| 비트율 변경 | 호출 비트율 변경 |
| 타이머 실행 | Ping 호출 |

## 구현 단계

1. **콘텐츠의 첫 번째 프레임이 화면에서 렌더링될 때 [세션 시작](../session/session-start.md) 후 [재생](play.md)**&#x200B;을 호출합니다. 또한 일시 중지 또는 버퍼 중지 후 재생이 다시 시작될 때 재생을 전송합니다. 별도의 다시 시작 이벤트가 없습니다.
1. 사용자가 재생을 일시 중지하면 **[일시 중지 시작](pause-start.md)**&#x200B;을 호출합니다. 재생이 다시 시작될 때 재생을 전송합니다.
1. 플레이어가 데이터 대기 중이면 **[버퍼 시작](buffer-start.md)**&#x200B;을 호출합니다. XDM 기반 API에서 버퍼 끝은 다음 재생 이벤트를 전송할 때 추론됩니다. Mobile SDK에서도 버퍼링이 확인될 때 명시적으로 `BufferComplete`을(를) 호출합니다.
1. **기본 콘텐츠 재생 중에는 10초마다, 광고 재생 중에는 1초마다 [Ping](ping.md)**&#x200B;을 호출합니다. Ping은 세션을 활성 상태로 유지하고 플레이헤드 이동을 기록합니다. Mobile SDK는 Ping을 자동으로 보냅니다. 다른 모든 플랫폼은 Ping을 수동으로 보내야 합니다.
1. 플레이어가 새 비트율을 협상할 때마다 **[비트율 변경](bitrate-change.md)**&#x200B;을 호출합니다. 백엔드가 [평균 비트율](/help/reporting/metrics/average-bitrate.md) 및 관련 품질 지표를 계산할 수 있도록 현재 QoE 데이터(비트율, 초당 프레임, 드롭된 프레임)를 포함합니다.
