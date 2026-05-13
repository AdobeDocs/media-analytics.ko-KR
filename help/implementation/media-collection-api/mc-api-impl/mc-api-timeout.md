---
title: 시간 제한 조건
description: Media Collection API 시간 제한 조건에 대해 알아봅니다.
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/13vwFrp3NF-e-odFn3eXIuhHusl14ovkwhTpPYbJC0U
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 165
ht-degree: 60%

---

# 시간 제한 조건{#timeout-conditions}

**Media Collection API 시간 제한 조건**

상태를 저장하지 않는 Media Collection API는 시간 제한 조건이 발생할 때 새 세션 ID를 발급할 Media SDK와 동일한 메커니즘을 가지고 있지 않습니다. 시간 제한 조건이 발생하면 백 엔드에서 세션을 닫고 해당 세션 ID로 수행된 모든 후속 호출이 삭제됩니다. 세션 시간 초과를 처리하는 논리는 클라이언트에서 처리해야 합니다. 즉, 플레이어는 시간 초과 조건을 모니터링하고, 시간 초과가 발생하는 경우 새 세션 ID를 얻어야 합니다.

* **10분: API 이벤트 없음**

  백 엔드에서 API 이벤트를 받지 못하면 세션을 닫습니다.
* **30분: 플레이헤드 변경 없음**

  플레이헤드가 30분 동안 이동하지 않으면(예: 사용자가 일시 정지를 누르고 감) 백 엔드에서 세션을 닫습니다.

>[!NOTE]
>
>세션을 `events` 이벤트 유형을 사용하여 `sessionEnd` 요청을 보내어 강제 종료할 수도 있습니다.
