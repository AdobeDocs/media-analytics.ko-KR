---
title: 플레이어 상태 추적 예
description: 이 항목에는 플레이어 상태 추적 기능의 예가 포함됩니다.
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 플레이어 상태 추적 예

예제 추가


## 긴 일시 중지 예

비디오 세션에 30분 이상의 일시 중지 시간이 있으면 API에 새 세션이 필요합니다. 이 경우 클라이언트는 새 세션 ID를 생성해야 합니다. 두 비디오 세션의 경우 클라이언트는 플레이어가 속한 모든 상태를 유지하고 모든 정보를 호출 직후 `stateStart` 이벤트로 `sessionStart` 전송해야 합니다.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd
`

이 `sessionEnd` 가 전송되면 새 비디오 세션을 시작해야 하며 첫 번째 API 이벤트는 다음과 같습니다.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

긴 일시 중지 예는 플레이어가 상태를 저장하므로 새 비디오 세션으로 전송할 수 있음을 보여줍니다.
