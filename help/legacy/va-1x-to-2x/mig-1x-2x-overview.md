---
title: 마이그레이션 개요
description: 1.x에서 2.x 버전의 Media SDK로 마이그레이션하는 방법에 대해 알아봅니다.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/mM6vZFyx6BG5MZXrzOc5hkBM6pOdzBCLiSL3WgON9LU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 235
ht-degree: 87%

---

# VHL 1.x에서 VHL 2.x로의 이전 마이그레이션 개요 {#migration-overview}

VHL 1.x에서 VHL 2.x로 마이그레이션하는 방법은 간단합니다. 새 버전이 초기화, 구성 및 플레이어 위임에 단순화된 API 기능을 제공하기 때문입니다

다음은 1.x와 2.x의 주요 차이점입니다.

* **플러그인, 대리자 -** Analytics, VideoPlayer 및 하트비트에 대해 더 이상 플러그인 및 대리자를 구현할 필요가 없습니다.
* **구성 -** 더 이상 1.x 플러그인에 대한 구성을 인스턴스화할 필요가 없습니다.

## 2.x의 이점 {#benefits-of-two-x}

* 모든 공개 메서드는 개발자가 쉽게 구현할 수 있도록 `MediaHeartbeat` 클래스에 통합되어 있습니다.
* 이제 모든 구성이 `MediaHeartbeatConfig` 클래스에 통합되어 있습니다.
* 더 이상 Analytics, VideoPlayer 및 하트비트 플러그인 구성을 인스턴스화할 필요가 없습니다. `MediaHeartbeatDelegate` 및 `MediaHeartbeatConfig` 인스턴스를 사용하여 `MediaHeartbeat` 클래스를 인스턴스화하기만 하면 됩니다. 이는 Media Analytics를 인스턴스화하는 데 필요한 유일한 구현입니다.

  Analytics 플러그인, VideoPlayer 플러그인 및 하트비트 플러그인에 대한 모든 구현을 `MediaHeartbeat`의 초기화로 안전하게 삭제할 수 있습니다. 또한 플러그인 배열에서 입력으로 가져오는 초기화에 대한 기존 구현을 모두 제거하십시오. 1.x 및 2.x 구현을 [코드 비교: 1.x와 2.x](./code-comparison-1x-2x.md)에서 나란히 비교한 것을 볼 수 있습니다.

2.x의 새 API는 다음에서 자세히 설명합니다. [API 1.x ~ 2.x 변환.](./1x-2x-api-change.md)
