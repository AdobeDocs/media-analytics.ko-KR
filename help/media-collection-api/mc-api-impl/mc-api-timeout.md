---
seo-title: 시간 제한 조건
title: 시간 제한 조건
uuid: 2 a 4 ea 13 e-a 561-4 adf-b 567-f 980301 b 32 c 8
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# 시간 제한 조건{#timeout-conditions}

**미디어 컬렉션 API 시간 초과 조건**

Stateless의 미디어 수집 API는 시간 제한 조건이 발생할 때 새 세션 ID를 발행하는 미디어 SDK와 동일한 메커니즘을 가지지 않습니다. 시간 제한 조건이 발생하면 백 엔드에서 세션을 닫고, 해당 세션 ID로 작성된 모든 후속 호출이 삭제됩니다. 세션 시간 제한을 처리하는 논리는 클라이언트에서 처리해야 합니다. 즉, 플레이어에서 시간 제한 조건을 모니터링하고, 시간 초과가 발생하면 새 세션 ID를 가져와야 합니다.

* **10 분: API 이벤트 없음**

   백엔드가 API 이벤트를 수신하지 못하면 세션이 닫힙니다.
* **30 분: 재생 헤드 변경 없음**

   재생 헤드가 30 분 동안 움직이지 않는 경우 (예: 사용자가 일시 정지 및 걸음 이동) 백엔드는 세션을 종료합니다.

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.

