---
title: 표준 및 사용자 지정 상태 정보
description: 표준 및 사용자 지정 플레이어 상태 구현 및 보고를 위한 요구 사항 및 지침을 비롯한 플레이어 상태 추적 기능에 대해 알아봅니다.
exl-id: 3c492055-d471-4147-aa78-b058d6b931f4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 92%

---

# 표준 및 사용자 지정 상태 정보

5개의 표준 플레이어 상태를 사용할 수 있으며 자체 사용자 지정 상태를 추가할 수 있습니다.

| 표준 상태 이름 | Media SDK 상수 | Media Collection API 이름 |
|-----------------------|------------------------------------------|-----------------------------|
| 전체 화면 | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| 자막 | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| 음소거 | `ADB.Media.PlayerState.Mute` | `mute` |
| 화면 속 화면 | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| 초점 | `ADB.Media.PlayerState.InFocus` | `inFocus` |

데이터는 표준 및 사용자 지정 상태에 대해 동일한 방법으로 계산되지만 Analytics 보고에 대해서는 데이터가 다르게 저장됩니다.

**표준 상태의 경우**- Analytics 보고(관리측)의 미디어 관리 콘솔에서 플레이어 상태 추적을 활성화하면 보고 및 데이터 내보내기에 15개의 솔루션 변수를 사용할 수 있습니다.

**사용자 지정 상태의 경우**- 자체 처리 규칙을 만들어 계산된 값을 사용자 지정 이벤트에 저장한 다음 보고 및 데이터 내보내기에 이러한 규칙을 사용할 수 있습니다.

## 지침

* 하나의 비디오 세션은 10개의 플레이어 상태로 제한됩니다.
* 상태의 모든 조합이 허용됩니다.
* 여러 플레이어 상태가 전달되면 첫 10개만 유지되어 다운스트림으로 VA 처리 구성 요소에 전달됩니다.
* 닫혀 있거나 그렇지 않은 상태에 상관없이 최대 10개 상태가 모든 상태에 적용됩니다.
* 한 상태는 여러 번 시작되고 종료될 수 있으며, 단일 상태로 계산됩니다. 예를 들어 `closedCapationing`을 5번 시작하고 중지할 수 있지만, 단일 상태로 계산됩니다.
* 최대 10개의 허용 상태를 초과하는 상태는 모두 무시됩니다.

## 사용자 지정 상태

사용자 지정 상태를 만드는 기능을 사용하면 재생 세션 중에 사용자 지정 동작을 캡처하고 사용자 지정 메타데이터를 업데이트할 수 있습니다.

사용자 지정 상태 만들기에 대한 자세한 내용은 [미디어 API 참조 안내서`createStateObject` ](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)를 참조하십시오.
