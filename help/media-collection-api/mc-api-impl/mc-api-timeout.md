---
title: 시간 제한 조건
description: 시간 제한 조건
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 100%

---

# 시간 제한 조건{#timeout-conditions}

**Media Collection API 시간 제한 조건**

상태를 저장하지 않는 Media Collection API는 시간 제한 조건이 발생할 때 새 세션 ID를 발급할 Media SDK와 동일한 메커니즘을 가지고 있지 않습니다. 시간 제한 조건이 발생하면 백 엔드에서 세션을 닫고, 해당 세션 ID로 작성된 모든 후속 호출이 삭제됩니다. 세션 시간 제한을 처리하는 논리는 클라이언트에서 처리해야 합니다. 즉, 플레이어에서 시간 제한 조건을 모니터링하고, 시간 초과가 발생하면 새 세션 ID를 가져와야 합니다.

* **10분: API 이벤트 없음**

   백 엔드에서 API 이벤트를 받지 못하면 세션을 닫습니다.
* **30분: 플레이헤드 변경 없음**

   플레이헤드가 30분 동안 이동하지 않으면(예: 사용자가 일시 정지를 누르고 감) 백 엔드에서 세션을 닫습니다.

>[!NOTE]
>
>세션을 `events` 이벤트 유형을 사용하여 `sessionEnd` 요청을 보내어 강제 종료할 수도 있습니다.
