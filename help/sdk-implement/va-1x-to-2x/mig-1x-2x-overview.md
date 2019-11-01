---
title: 마이그레이션 개요
description: 이 항목에서는 Media SDK의 1.x에서 2.x 버전으로 마이그레이션하는 방법에 대한 개요를 제공합니다.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 마이그레이션 개요{#migration-overview}

VHL 1.x에서 VHL 2.x로 마이그레이션하는 방법은 간단합니다. 새 버전이 초기화, 구성 및 플레이어 위임에 단순화된 API 기능을 제공하기 때문입니다.

다음은 1.x와 2.x의 주요 차이점입니다.

* **플러그인, 위임 -** 더 이상 Analytics, VideoPlayer 및 하트비트에 대한 플러그인 및 위임을 구현할 필요가 없습니다.
* **구성 -** 1.x 플러그인에 대한 구성을 인스턴스화할 필요가 없습니다.

## 2.x의 이점 {#benefits-of-two-x}

* All of the public methods are consolidated into the `MediaHeartbeat` class to make implementation easier on developers.
* All configs are now consolidated into the `MediaHeartbeatConfig` class.
* 더 이상 Analytics, VideoPlayer 및 하트비트 플러그인에 대한 구성을 인스턴스화할 필요가 없습니다. 클래스를 `MediaHeartbeat` 및 `MediaHeartbeatDelegate` `MediaHeartbeatConfig` 인스턴스로 인스턴스화하기만 하면 됩니다. 이는 미디어 분석을 초기화하는 데 필요한 유일한 구현입니다.

   With the initialization of `MediaHeartbeat`, you can safely delete all of the implementation for Analytics Plugin, VideoPlayer Plugin, and Heartbeat Plugin. 또한 플러그인 배열에서 입력으로 가져오는 초기화에 대한 기존 구현을 모두 제거하십시오. You can see side-by-side comparisons of the 1.x and 2.x implementations here: [Code comparison: 1.x to 2.x.](./code-comparison-1x-2x.md)

2.x의 새 API는 다음에서 자세히 설명합니다. [API 1.x ~ 2.x 변환.](./1x-2x-api-change.md)
