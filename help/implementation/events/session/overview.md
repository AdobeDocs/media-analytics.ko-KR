---
title: 컨텐츠 재생 추적
description: 미디어 로드, 미디어 시작, 미디어 일시 중지, 미디어 완료 추적을 포함하여 코어 재생 추적에 대해 알아봅니다.
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/cHrkCe0mQm8GlHwLVgf4cjF0VM8B1r3CRt39I2LB6kk
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889beid: e992d880-33bc-4949-a648-aa7d410276cd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 803
ht-degree: 2%

---


# 컨텐츠 재생 추적

코어 재생 추적에는 미디어 로드, 시작, 일시 중지, 다시 시작, 완료 및 세션 종료가 포함됩니다. 필수는 아니지만 버퍼링 및 찾기 추적도 전체 재생 구현의 핵심 구성 요소입니다.

## 플레이어 이벤트

| 플레이어 이벤트 | 액션 |
| --- | --- |
| 미디어 로드 | 미디어 개체 만들기, SessionStart 호출 |
| 미디어 시작 | 통화 재생 |
| 일시 정지 | PauseStart 호출 |
| 일시 중단에서 다시 시작 | 통화 재생 |
| 미디어 완료 | SessionComplete 호출 |
| 미디어 중단/언로드 | SessionEnd 호출 |
| 버퍼링 시작 | BufferStart 호출 |
| 버퍼링 종료 | 통화 재생(다시 시작) |
| 찾기 시작 | SeekStart 호출 |
| 찾기 종료 | SeekComplete를 호출한 다음 Play를 호출합니다. |

## 구현 단계

1. **사용자가 재생을 트리거하는 시점을 식별합니다**(사용자가 재생을 클릭하거나 자동 재생이 실행됨). 컨텐츠 이름, ID, 길이, 스트림 유형 및 미디어 유형으로 미디어 개체를 만듭니다. 필드 정의는 [콘텐츠 이름](/help/implementation/variables/core/content-name.md), [콘텐츠 ID](/help/implementation/variables/core/content-id.md), [콘텐츠 길이](/help/implementation/variables/core/content-length.md), [스트림 유형](/help/implementation/variables/core/stream-type.md) 및 [콘텐츠 유형](/help/implementation/variables/core/content-type.md)을 참조하십시오.
1. **메타데이터 첨부** — 표준 메타데이터(쇼, 시즌, 에피소드 등) 및 사용자 지정 컨텍스트 데이터 변수 간에 상관 관계를 설정할 수도 있습니다. 표준 메타데이터 키 참조에 대해서는 [표시](/help/implementation/variables/standard-metadata/show.md), [시즌](/help/implementation/variables/standard-metadata/season.md), [에피소드](/help/implementation/variables/standard-metadata/episode.md), [장르](/help/implementation/variables/standard-metadata/genre.md) 및 [네트워크](/help/implementation/variables/standard-metadata/network.md)를 참조하십시오.
1. **세션 추적을 시작하려면 [세션 시작](/help/implementation/events/session/session-start.md)**&#x200B;을 호출합니다. 이렇게 하면 데이터와 메타데이터가 로드되고 QoS 측정을 시작할 시간이 시작됩니다. SessionStart는 첫 번째 프레임이 아닌 재생할 *intent*&#x200B;을(를) 추적합니다.
1. **화면에서 콘텐츠의 첫 번째 프레임이 렌더링될 때 [재생](/help/implementation/events/playback/play.md)**&#x200B;을 호출합니다.
1. 플레이어가 일시 중지되면 **[일시 중지 시작](/help/implementation/events/playback/pause-start.md)**&#x200B;을 호출합니다. 재생이 다시 시작되면 Play 를 다시 호출합니다. 별도의 다시 시작 이벤트가 없습니다.
1. 뷰어가 콘텐츠의 끝에 도달하면 **[세션 완료](/help/implementation/events/session/session-complete.md)**&#x200B;를 호출합니다.
1. 플레이어가 언로드되거나 뷰어가 끝에 도달하지 않고 콘텐츠를 중단하면 **[세션 종료](/help/implementation/events/session/session-end.md)**&#x200B;를 호출합니다. SessionEnd는 세션을 즉시 닫습니다. 이후 추가 이벤트를 추적할 수 없습니다.

>[!IMPORTANT]
>
>추적 세션의 끝을 `SessionEnd`는 표시합니다. 세션을 끝까지 성공적으로 시청한 경우 `SessionEnd` 전에 `SessionComplete`을(를) 호출하십시오. 새 세션에 대한 `SessionStart`을(를) 제외하고, 다른 모든 추적 호출은 `SessionEnd` 이후에 무시됩니다.

## 코어 재생

다음 예는 세션 시작부터 컨텐츠 완료 및 세션 종료까지의 전체 세션 흐름을 보여줍니다.

플랫폼별 구현 세부 정보는 [세션 시작](/help/implementation/events/session/session-start.md), [재생](/help/implementation/events/playback/play.md), [일시 중지 시작](/help/implementation/events/playback/pause-start.md), [세션 완료](/help/implementation/events/session/session-complete.md) 및 [세션 종료](/help/implementation/events/session/session-end.md)를 참조하십시오.

## 버퍼링

버퍼 시작 신호는 플레이어가 데이터를 기다리고 있음을 나타냅니다. 버퍼 종료는 BufferStart(XDM 기반 API) 후에 재생 이벤트를 전송할 때 추론됩니다. 모바일 SDK에서 BufferComplete를 명시적으로 호출하기도 합니다.

구현 세부 정보는 [버퍼 시작](/help/implementation/events/playback/buffer-start.md)을 참조하십시오.

## 찾기

검색 시작 신호는 뷰어가 스크러빙하고 있습니다. 콘텐츠 재생을 재개하려면 찾기를 종료한 후 재생 을 선택하십시오.

구현 세부 정보는 [일시 중지 시작](/help/implementation/events/playback/pause-start.md)(검색 시작) 및 [재생](/help/implementation/events/playback/play.md)(검색 종료)을 참조하십시오.

## 앱 중단 처리

미디어 애플리케이션에서의 재생은 다양한 방식으로 중단될 수 있습니다. 즉, 사용자가 일시 정지를 누르고 앱이 백그라운드로 전환되고, 전화 통화가 도착합니다. 원인에 관계없이 추적 지침은 다음과 같습니다.

1. 응용 프로그램이 중단되면 **PauseStart**&#x200B;를 호출합니다(배경으로 이동, 미디어 일시 중지 등).
1. 애플리케이션이 전경으로 돌아가거나 미디어가 재생을 재개하면 **재생**&#x200B;을 호출합니다.

>[!NOTE]
>
>앱이 배경에서 반환되면 SessionStart를 호출하지 마십시오. SessionStart를 호출하면 해당 지점까지의 재생이 총 재생 시간에 계산되지 않고, 이전 진행률 마커, 세그먼트 및 챕터 경계가 손실됩니다.

**일시 중지된 세션이 언제 종료되어야 합니까?** 애플리케이션에서 배경 재생을 허용하지 않는 경우 즉시 PauseStart를 호출한 다음 백그라운드에서 약 1분 후 SessionEnd를 호출합니다. 애플리케이션에서 백그라운드에서 일시 중지 ping을 계속 전송할 수 없으며 세션을 무기한 열어 두면 좋지 않은 경험이 제공됩니다. 애플리케이션이 배경 재생(오디오 앱, 비디오 팟캐스트 앱)을 지원하는 경우 백그라운드에서 Ping을 계속 전송합니다.

**긴 백그라운드 기간이 지난 후 다시 시작:** 앱이 세션이 만료될 만큼 오래 백그라운드에 있으면(30분 동안 비활성) SessionEnd를 호출하여 느린 세션을 완전히 닫은 다음 뷰어가 돌아오면 SessionStart를 호출하여 새 세션을 시작합니다.

## 비활성 세션 다시 시작

10분 동안 이벤트가 수신되지 않거나 30분 동안 플레이헤드 이동이 없는 경우 세션이 자동으로 만료됩니다. 세션이 만료된 후 사용자가 돌아오면 SessionStart 를 다시 호출하여 새 세션을 엽니다.

**장치 간 다시 시작(장치 간 전달):** 뷰어가 장치 간에 재생을 전송할 때(예: 전화에서 TV로 캐스팅) 다시 시작 플래그를 사용하여 Analytics 보고에서 세션을 함께 연결합니다.

1. **소스 장치**&#x200B;에서 뷰어가 캐스트를 시작하면 SessionEnd를 호출합니다. SessionComplete를 호출하지 않습니다. 콘텐츠가 완료되지 않았습니다.
1. **대상 장치**&#x200B;에서 다시 시작 플래그를 `true`(으)로 설정하여 SessionStart를 호출하고 동일한 콘텐츠 메타데이터와 플레이헤드 위치를 원본 장치에서 전달합니다.

다시 시작 플래그를 설정하면 Analytics가 핸드오프의 두 번째 단계에서 [미디어 시작](/help/reporting/metrics/media-starts.md)이 아닌 [콘텐츠 다시 시작](/help/reporting/metrics/content-resumes.md)을(를) 증가시킵니다.

**이전에 닫은 세션을 수동으로 다시 시작:** 응용 프로그램에서 사용자 데이터를 저장하고 이전에 닫은 세션을 다시 시작할 수 있는 경우 세션 시작 시 다시 시작 플래그를 설정합니다. 모든 플랫폼에 대한 구현 세부 정보는 [세션 시작](/help/implementation/events/session/session-start.md#resuming-a-session)을 참조하세요.
