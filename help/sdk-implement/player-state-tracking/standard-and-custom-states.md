---
title: 표준 및 사용자 지정 상태 정보
description: 이 항목에서는 표준 및 사용자 정의 플레이어 상태를 구현 및 보고하기 위한 요구 사항 및 지침을 포함한 플레이어 상태 추적 기능에 대해 설명합니다.
translation-type: tm+mt
source-git-commit: f7a45dfbabe71fa9e1de7a4f4b2a7e64849e4ef4
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 1%

---


# 표준 및 사용자 지정 상태 정보

5개의 표준 플레이어 상태를 사용할 수 있으며 사용자 정의 상태를 추가할 수 있습니다.

| 표준 상태 이름 | 미디어 SDK 상수 | Media Collection API 이름 |
|-----------------------|------------------------------------------|-----------------------------|
| 전체 화면 | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| 자막 | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| 음소거 | `ADB.Media.PlayerState.Mute` | `mute` |
| 사진 속 사진 | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| 초점 | `ADB.Media.PlayerState.InFocus` | `inFocus` |

데이터는 표준 및 사용자 지정 상태에 대해 동일한 방법으로 계산되지만 Analytics 보고에 대해서는 데이터가 다르게 저장됩니다.

**표준 상태**- Analytics 보고(관리측)의 미디어 관리 콘솔에서 플레이어 상태 추적을 활성화하면 보고 및 데이터 내보내기에 15개의 솔루션 변수를 사용할 수 있습니다.

**사용자 지정 상태**- 자체 처리 규칙을 만들어 계산된 값을 사용자 지정 이벤트에 저장한 다음 보고 및 데이터 내보내기에 이러한 규칙을 사용할 수 있습니다.

## 지침

* 한 비디오 세션은 10개의 플레이어 상태로 제한됩니다.
* 모든 주의 조합이 허용된다.
* 여러 플레이어 상태가 전달되면, 처음 10개만 유지되어 다운스트림으로 VA 처리 구성 요소로 전달됩니다.
* 닫혀 있거나 없는 상태에 상관없이 최대 10개 상태가 모든 상태에 적용됩니다.
* 상태는 여러 번 시작 및 종료될 수 있으며 단일 상태로 계산됩니다. 예를 들어 5번 시작 및 중지할 `closedCapationing` 수 있지만 단일 상태로 계산됩니다.
* 최대 허용 상태를 10개 초과하는 모든 상태는 무시됩니다.

## 사용자 지정 상태

사용자 정의 상태를 만드는 기능을 사용하면 재생 세션 중에 사용자 정의 동작을 캡처하고 사용자 정의 메타데이터를 업데이트할 수 있습니다.

사용자 지정 상태 만들기에 대한 자세한 내용은 [미디어 API 참조 안내서를 참조하십시오. `createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
