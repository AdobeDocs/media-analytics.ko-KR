---
title: 마이그레이션 개요
description: 이 항목에서는 Media SDK 1.x에서 2.x 버전으로 마이그레이션하는 방법에 대한 개요를 제공합니다.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 마이그레이션 개요{#migration-overview}

VHL 1.x에서 VHL 2.x로 마이그레이션하는 방법은 간단합니다. 새 버전이 초기화, 구성 및 플레이어 위임에 단순화된 API 기능을 제공하기 때문입니다.

다음은 1.x와 2.x의 주요 차이점입니다.

* **플러그인, 위임 -** 더 이상 Analytics, VideoPlayer 및 하트비트에 대한 플러그인 및 위임을 구현할 필요가 없습니다.
* **구성 -** 1.x 플러그인에 대한 구성을 인스턴스화할 필요가 없습니다.

## 2.x의 이점 {#benefits-of-two-x}

* 모든 공개 메서드는 개발자가 쉽게 구현할 수 있도록 `MediaHeartbeat` 클래스에 통합되어 있습니다.
* 이제 모든 구성이 `MediaHeartbeatConfig` 클래스에 통합되어 있습니다.
* 더 이상 Analytics, VideoPlayer 및 하트비트 플러그인 구성을 인스턴스화할 필요가 없습니다. `MediaHeartbeatDelegate` 및 `MediaHeartbeatConfig` 인스턴스를 사용하여 `MediaHeartbeat` 클래스를 인스턴스화하기만 하면 됩니다. 이는 Media Analytics를 인스턴스화하는 데 필요한 유일한 구현입니다.

   Analytics 플러그인, VideoPlayer 플러그인 및 하트비트 플러그인에 대한 모든 구현을 `MediaHeartbeat`의 초기화로 안전하게 삭제할 수 있습니다. 또한 플러그인 배열에서 입력으로 가져오는 초기화에 대한 기존 구현을 모두 제거하십시오. 1.x 및 2.x 구현을 [코드 비교: 1.x와 2.x](./code-comparison-1x-2x.md)에서 나란히 비교한 것을 볼 수 있습니다.

2.x의 새 API는 다음에서 자세히 설명합니다. [API 1.x ~ 2.x 변환.](./1x-2x-api-change.md)
