---
title: 플레이어 상태 추적
description: 플레이어 상태 이벤트와 전체 화면, 음소거, 자막, PIP(Picture-in-Picture) 및 인포커스 상태를 추적하는 방법에 대해 알아봅니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 12%

---


# 플레이어 상태 추적

플레이어 상태 이벤트는 뷰어가 세션 전체에서 플레이어 컨트롤과 상호 작용하는 방법을 추적합니다. 이 매개 변수는 선택 사항이며 코어 미디어 추적 구현에 필요하지 않습니다. 추적할 수 있는 5개 상태는 `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` 및 `inFocus`입니다.

플레이어 상태 이벤트는 뷰어가 자막 또는 음소거를 활성화하는 빈도와 같은 접근성 기능 사용을 이해하는 데 유용합니다. 또한 전체 화면 대 인라인 보기 및 PIP(Picture-in-Picture) 멀티태스킹과 같은 보기 비헤이비어 패턴을 보여줍니다.

## 플레이어 이벤트

| 플레이어 이벤트 | 액션 |
| --- | --- |
| 플레이어가 상태에 들어갑니다. | 호출 상태 시작 |
| 플레이어가 상태를 종료합니다. | 호출 상태 종료 |

## 표준 및 사용자 정의 상태

5개의 표준 플레이어 상태를 사용할 수 있으며 자체 사용자 지정 상태를 추가할 수 있습니다.

| 표준 상태 이름 | Media SDK 상수 | Media Collection API 이름 |
|----|----|----|
| 전체 화면 | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| 자막 | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| 음소거 | `ADB.Media.PlayerState.Mute` | `mute` |
| 화면 속 화면 | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| 포커스 | `ADB.Media.PlayerState.InFocus` | `inFocus` |

XDM 경로 및 지표 정의를 포함한 전체 변수 참조에 대해서는 [플레이어 상태 변수](/help/implementation/variables/player-state/)를 참조하십시오.

**사용자 지정 상태:** 사용자 지정 상태를 만들어 응용 프로그램과 관련된 추가 플레이어 동작을 캡처할 수 있습니다. 사용자 지정 상태 개체를 만드는 방법에 대한 자세한 내용은 [Media API 참조: `createStateObject`](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/)을(를) 참조하십시오.

## 구현 단계

1. 플레이어가 추적 가능한 5개 상태 중 하나를 입력하면 **[상태 시작](state-start.md)**&#x200B;을 호출합니다. 여러 상태를 동시에 활성화할 수 있으며 여러 상태를 동일한 이벤트 호출에서 시작할 수 있습니다.
1. 플레이어가 상태를 종료하면 **[상태 종료](state-end.md)**&#x200B;를 호출합니다. 여러 상태를 동일한 이벤트 호출에서 종료할 수 있으며 상태를 단일 호출에서 함께 시작하고 종료할 수 있습니다.

## 지침

* 하나의 비디오 세션은 10개의 플레이어 상태로 제한됩니다.
* 상태의 모든 조합이 허용됩니다.
* 여러 플레이어 상태가 전달되면 첫 10개만 유지되어 다운스트림으로 미디어 백엔드에 전달됩니다.
* 열렸는지 닫혔는지에 상관없이 최대 10개의 상태가 모든 상태에 적용됩니다.
* 상태는 여러 번 시작되고 종료될 수 있으며, 단일 상태로 계산됩니다. 예를 들어 `closedCaptioning`을(를) 5번 시작하고 중지할 수 있지만, 하나의 상태로 계산됩니다.
* 플레이어 상태는 모든 재생 상태에 대해 계산됩니다(분할 없음).
* 플레이어 상태는 각 개별 재생 세션에 대해 캡처됩니다. 플레이어 상태는 재생 간에 계산되지 않습니다.
* 상태가 중지된 후에는 애플리케이션 상태에 대한 지식이 유지되지 않습니다. 상태가 종료된 후에는 상태를 다시 시작해야 추적을 계속할 수 있습니다.

## 여러 상태를 동시에 업데이트

XDM 기반 플랫폼에서 여러 상태 변경 사항을 `statesStart` 및 `statesEnd`의 배열을 사용하여 단일 `statesUpdate` 호출로 일괄 처리할 수 있습니다. Mobile SDK에서 각 상태를 변경하려면 별도의 호출이 필요합니다.

다음 예제에서는 음소거와 PIP(Picture-in-Picture)를 함께 시작한 다음 전체 화면으로 전환합니다.

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

```javascript
// t0 — start mute and picture-in-picture together
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }, { name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t1 — end mute and picture-in-picture; start full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "mute" }, { name: "pictureInPicture" }],
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t2 — end full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Mobile SDK은 일괄 처리를 지원하지 않습니다. 각 상태 변경에 대해 별도의 호출을 전송하십시오.

```swift
// t0 — start mute and picture-in-picture
let muteState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.MUTE)
let pipState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(event: MediaEvent.StateStart, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateStart, info: pipState, metadata: nil)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateEnd, info: pipState, metadata: nil)
let fullscreenState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(event: MediaEvent.StateStart, info: fullscreenState, metadata: nil)

// t2 — end full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: fullscreenState, metadata: nil)
```

>[!TAB Android]

Mobile SDK은 일괄 처리를 지원하지 않습니다. 각 상태 변경에 대해 별도의 호출을 전송하십시오.

```kotlin
// t0 — start mute and picture-in-picture
val muteState = Media.createStateObject(MediaConstants.PlayerState.MUTE)
val pipState = Media.createStateObject(MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(Media.Event.StateStart, muteState, null)
tracker.trackEvent(Media.Event.StateStart, pipState, null)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(Media.Event.StateEnd, muteState, null)
tracker.trackEvent(Media.Event.StateEnd, pipState, null)
val fullscreenState = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(Media.Event.StateStart, fullscreenState, null)

// t2 — end full screen
tracker.trackEvent(Media.Event.StateEnd, fullscreenState, null)
```

>[!TAB Roku Edge]

```brightscript
' t0 — start mute and picture-in-picture together
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "playhead": 0
        }
    }
})

' t1 — end mute and picture-in-picture; start full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "statesStart": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})

' t2 — end full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})
```

>[!TAB 미디어 Edge API]

```sh
# t0 — start mute and picture-in-picture together
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:00:00+00:00"
    }
  }]
}'

# t1 — end mute and picture-in-picture; start full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "statesStart": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:01:00+00:00"
    }
  }]
}'

# t2 — end full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:02:00+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## 이전 구현 유형(Analytics 전용)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

여러 상태를 변경하려면 별도의 호출이 필요합니다.

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
var pipState = ADB.Media.createStateObject(ADB.Media.PlayerState.PictureInPicture);
tracker.trackPlayerStateStart(muteState);
tracker.trackPlayerStateStart(pipState);

// t1 — end mute and picture-in-picture; start full screen
tracker.trackPlayerStateEnd(muteState);
tracker.trackPlayerStateEnd(pipState);
var fullscreenState = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);
tracker.trackPlayerStateStart(fullscreenState);

// t2 — end full screen
tracker.trackPlayerStateEnd(fullscreenState);
```

>[!TAB Chromecast]

여러 상태를 변경하려면 별도의 호출이 필요합니다.

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.Mute);
var pipState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.PictureInPicture);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, pipState, null);

// t1 — end mute and picture-in-picture; start full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, pipState, null);
var fullscreenState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, fullscreenState, null);

// t2 — end full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, fullscreenState, null);
```

>[!TAB Roku 2.x]

플레이어 상태 추적은 Roku 2.x SDK에서 사용할 수 없습니다. 플레이어 상태를 추적하려면 [Roku Edge SDK](/help/implementation/edge/roku.md)를 사용하십시오.

>[!TAB 미디어 컬렉션 API]

```json
// t0 — start mute and picture-in-picture together
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999130627 }
}

// t1 — end mute and picture-in-picture; start full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ],
    "statesStart": [
      { "media.state.name": "fullScreen" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999230627 }
}

// t2 — end full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [{ "media.state.name": "fullScreen" }]
  },
  "playerTime": { "playhead": 0, "ts": 1569999330627 }
}
```

>[!ENDTABS]

## 긴 일시 중지

비디오 세션에 30분 이상의 일시 중지 시간이 있으면 API에 새 세션이 필요합니다. 새 `sessionStart` 호출 직후 `stateStart` 이벤트로 복원할 수 있도록 새 세션 ID를 생성하고 모든 활성 상태를 유지합니다.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

`sessionEnd`을(를) 보낸 후 새 세션을 시작하고 즉시 활성 상태를 다시 보냅니다.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

## 상태 지표

추적된 각 상태에 대해 세 개의 지표가 계산되고 미디어 닫기 호출 시 Adobe Analytics으로 전송됩니다.

| 지표 | 컨텍스트 데이터 키 | 설명 |
| --- | --- | --- |
| 상태 설정 | `a.media.states.[state.name].set = true` | 재생 중에 상태가 한 번 이상 설정된 경우 `true` |
| 상태 수 | `a.media.states.[state.name].count = 4` | 재생 도중 상태가 발생한 횟수 |
| 상태 시간 | `a.media.states.[state.name].time = 240` | 재생 중 상태에서 체류한 총 시간(초) |
