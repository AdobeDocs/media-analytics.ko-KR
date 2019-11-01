---
title: 시간 제한 조건
description: null
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 시간 제한 조건{#timeout-conditions}

**Media Collection API 시간 초과 조건**

Media Collection API는 상태 비저장(상태 비저장)인 경우 시간 초과 조건이 발생하면 새 세션 ID를 발급하는 미디어 SDK와 동일한 메커니즘을 가지고 있지 않습니다. 시간 제한 조건이 발생하면 백 엔드에서 세션을 닫고, 해당 세션 ID로 작성된 모든 후속 호출이 삭제됩니다. 세션 시간 제한을 처리하는 논리는 클라이언트에서 처리해야 합니다. 즉, 플레이어에서 시간 제한 조건을 모니터링하고, 시간 초과가 발생하면 새 세션 ID를 가져와야 합니다.

* **10분:API 이벤트 없음**

   백 엔드가 API 이벤트를 수신하지 않으면 세션이 닫힙니다.
* **30분:재생 헤드 변경 없음**

   재생 헤드가 30분 동안 이동하지 않는 경우(예: 사용자가 일시 중지를 히트 후 걸어가짐) 백엔드가 세션을 닫습니다.

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.

