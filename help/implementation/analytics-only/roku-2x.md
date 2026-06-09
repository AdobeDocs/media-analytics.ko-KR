---
title: 스트리밍 미디어용 Roku 2.x 설정
description: SceneGraph 채널을 비롯한 Analytics 전용 스트리밍 미디어 구현을 위한 Roku용 Adobe Media SDK 2.x를 설치하고 구성합니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 2%

---

# 스트리밍 미디어용 Roku 2.x 설정

Roku(`adbmobile.brs`)용 Adobe Media SDK 2.x는 BrightScript로 작성된 Roku 채널의 스트리밍 미디어 데이터를 Adobe Analytics으로 직접 전송합니다. 또한 Audience Manager을 통해 대상 데이터를 수집하고 미디어 이벤트를 통해 참여를 측정합니다.

>[!NOTE]
>
>이 페이지에서는 Roku용 Analytics 전용 Media SDK 2.x에 대해 설명합니다. 새로운 구현의 경우 Adobe에서는 Adobe Analytics 외에도 Customer Journey Analytics, Adobe Journey Optimizer 및 Real-Time CDP에서 데이터를 사용할 수 있도록 하는 [Roku Edge SDK](/help/implementation/edge/roku.md)을(를) 권장합니다.

* **필수 구성 요소**:
   * [Analytics 전용 구현 개요](overview.md)를 완료합니다.
   * [Roku용 Media SDK을 다운로드합니다](/help/getting-started/download-sdks.md).
   * 미디어 플레이어에서 플레이어 이벤트를 구독하기 위한 API와 미디어 이름 및 플레이헤드 위치와 같은 플레이어 정보를 제공하는 API를 포함합니다.

## SDK 설치

`AdobeMobileLibrary-2.*-Roku.zip` 다운로드에는 다음 두 가지 구성 요소가 포함되어 있습니다.

* `adbmobile.brs`: 라이브러리 파일입니다. 채널의 `pkg:/source/` 디렉터리에 복사합니다.
* `ADBMobileConfig.json`: 앱에 맞게 사용자 지정된 SDK 구성 파일입니다.

SceneGraph 채널의 경우 `adbmobileTask.brs` 및 `adbmobileTask.xml`도 `pkg:/components/` 디렉터리에 복사합니다. [SceneGraph 지원](#scenegraph)을 참조하십시오.

## ADBMobileConfig.json 구성

구성 JSON에는 스트리밍 미디어에 대한 전용 `mediaHeartbeat` 키가 있습니다. 프로젝트 소스에 `ADBMobileConfig.json`을(를) 추가하고 `mediaHeartbeat`, `marketingCloud` 및 `analytics` 값을 설정합니다.

```json
{
  "analytics": {
    "rsids": "your-report-suite-id",
    "server": "your-analytics-server"
  },
  "marketingCloud": {
    "org": "YOUR-MCORG-ID@AdobeOrg"
  },
  "mediaHeartbeat": {
    "server": "your-namespace.hb-api.omtrdc.net",
    "publisher": "your-publisher-id",
    "channel": "sample-channel",
    "ssl": true,
    "ovp": "sample-ovp",
    "sdkVersion": "sample-sdk",
    "playerName": "Roku Player"
  }
}
```

| 구성 매개 변수 | 설명 |
| --- | --- |
| `server` | 미디어 추적 끝점의 URL. [Analytics 전용 구현 개요](overview.md)를 참조하세요. |
| `publisher` | 콘텐츠 게시자 고유 식별자. |
| `channel` | 컨텐츠 배포 채널의 이름입니다. [콘텐츠 채널](/help/implementation/variables/core/content-channel.md)(으)로 보고되었습니다. |
| `ssl` | 추적 호출에 SSL이 사용되는지 여부. |
| `ovp` | 온라인 비디오 플랫폼 공급자의 이름입니다. |
| `sdkVersion` | 앱 또는 SDK의 현재 버전입니다. |
| `playerName` | 플레이어 이름. [콘텐츠 플레이어 이름](/help/implementation/variables/core/content-player-name.md)(으)로 보고되었습니다. |

>[!IMPORTANT]
>
>`mediaHeartbeat`이(가) 잘못 구성된 경우 미디어 모듈은 오류 상태에 들어가고 추적 호출 전송을 중단합니다. `marketingCloud.org` 값에 `@AdobeOrg`이(가) 포함되어 있는지 확인하십시오.

## SDK 초기화 및 메시지 처리

`ADBMobile()`을(를) 사용하여 SDK 인스턴스를 가져옵니다. Experience Cloud 방문자 ID 서비스는 모든 히트에 포함된 방문자 ID를 생성합니다.

>[!IMPORTANT]
>
>SDK에서 ping을 제대로 보낼 수 있도록 250ms마다 기본 이벤트 루프에서 `processMessages` 및 `processMediaMessages`을(를) 호출합니다.

```brightscript
adb = ADBMobile()

' In your main event loop, every ~250 ms:
adb.processMessages()
adb.processMediaMessages()
```

| 메서드 | 설명 |
| --- | --- |
| `processMessages` | 큐에 있는 Analytics 이벤트를 SDK에 전달합니다. |
| `processMediaMessages` | 자동 Ping을 포함하여 큐에 있는 미디어 이벤트를 SDK에 전달합니다. |

## 미디어 이벤트 추적

해당 SDK 메서드를 호출하여 각 미디어 이벤트를 추적합니다. 정확한 호출, 빌더 및 상수는 각 [이벤트](/help/implementation/events/overview.md) 및 [변수](/help/implementation/variables/overview.md) 페이지에서 **Roku 2.x** 탭을 참조하십시오.

일반적인 세션은 미디어 개체를 빌드하고 `mediaTrackSessionStart`을(를) 호출하여 시작합니다.

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("Mr. Robot", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

contextData = { "a.media.show": "Mr. Robot" }

adb.mediaTrackSessionStart(mediaInfo, contextData)
```

글로벌 `adb_media_init_*` 빌더는 추적 호출에 사용되는 미디어, 광고, 광고 브레이크, 챕터 및 QoS 개체를 만듭니다.

| 빌더 | 서명 |
| --- | --- |
| 미디어 | `adb_media_init_mediainfo(name, id, length, streamType, mediaType)` |
| 광고 | `adb_media_init_adinfo(name, id, position, length)` |
| 광고 브레이크 | `adb_media_init_adbreakinfo(name, startTime, position)` |
| 챕터 | `adb_media_init_chapterinfo(name, position, length, startTime)` |
| QoS | `adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)` |

표준 메타데이터는 `a.media.*` 키의 연관 배열로 전달됩니다(SDK은 이러한 키에 대해 `MEDIA_VideoMetadataKeySHOW`과(와) 같은 명명된 상수도 정의함). 각 차원에 해당하는 키는 [변수](/help/implementation/variables/overview.md) 페이지를 참조하십시오.

## Experience Cloud 방문자 ID, 개인 정보 보호 및 로깅 구성

`ADBMobile()` 인스턴스의 다음 메서드는 ID, 개인 정보 및 디버깅을 관리합니다.

| 메서드 | 설명 |
| --- | --- |
| `visitorMarketingCloudID()` | Experience Cloud ID(ECID)를 검색합니다. |
| `visitorSyncIdentifiers(identifiers)` | 동일한 방문자에 대한 추가 고객 ID를 설정합니다. |
| `setAdvertisingIdentifier(rida)` | RIDA(Advertising)에 대한 Roku ID를 설정합니다. Roku [`getRIDA()`](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) API로 가져옵니다. |
| `getAllIdentifiers()` | Analytics, 방문자, Audience Manager 및 사용자 지정 식별자를 포함하여 SDK에 저장된 모든 식별자를 반환합니다. |
| `setPrivacyStatus(status)` | 개인 정보 상태를 설정합니다. `adb.PRIVACY_STATUS_OPT_IN` 또는 `adb.PRIVACY_STATUS_OPT_OUT`을(를) 전달합니다. [개인 정보](/help/implementation/opt-out-privacy.md)를 참조하세요. |
| `getPrivacyStatus()` | 현재 개인 정보 상태를 반환합니다. |
| `setDebugLogging(flag)` | 디버그 로깅을 활성화하거나 비활성화합니다. |
| `getDebugLogging()` | 디버그 로깅이 활성화된 경우 `true`을 반환합니다. |

## SceneGraph 지원 {#scenegraph}

SDK은 SceneGraph 앱에서 사용할 수 없는 구성 요소(예: 스레드)를 사용하므로 Roku SceneGraph XML 프레임워크는 기존 BrightScript SDK API를 직접 호출할 수 없습니다. 이러한 간극을 메우기 위해 SDK은 동일한 API를 노출하는 SceneGraph 호환 인스턴스를 반환하는 커넥터와 데이터를 반환하는 API에 대한 콜백 메커니즘을 제공합니다.

그 다리는 세 부분으로 이루어져 있다:

* **`adbmobileTask`노드**: 백그라운드 스레드에서 SDK API를 실행하고 데이터를 장면으로 반환하는 SceneGraph 작업 노드입니다.
* **커넥터 인스턴스**: 모든 레거시 공용 API를 래핑하고 `adbmobileTask` 노드와 통신합니다.
* **`API_RESPONSE`callback**: getter API에서 반환 값을 받는 데 사용되는 앱의 필드입니다.

SceneGraph 채널에서 SDK을 초기화하려면 다음을 수행하십시오.

1. 장면으로 `adbmobile.brs` 가져오기:

   ```brightscript
   <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
   ```

1. `adbmobileTask` 노드를 만들고 커넥터 인스턴스를 가져온 다음 SceneGraph 상수를 로드합니다.

   ```brightscript
   m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
   m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
   m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
   ```

1. 데이터를 반환하는 API에 대한 응답 개체를 수신할 콜백을 등록합니다.

   ```brightscript
   m.adbmobileTask.ObserveField(m.adbmobileConstants.API_RESPONSE, "onAdbmobileApiResponse")
   
   function onAdbmobileApiResponse() as void
       responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE]
       if responseObject <> invalid
           methodName = responseObject.apiName
           retVal = responseObject.returnValue
           if methodName = m.adbmobileConstants.PRIVACY_STATUS
               print "Privacy status: " + retVal
           end if
       end if
   end function
   ```

커넥터 인스턴스(`m.adbmobile`)는 기존 SDK(`mediaTrackSessionStart`, `mediaTrackPlay`, `mediaTrackPause`, `mediaTrackComplete`, `mediaTrackSessionEnd`, `mediaTrackError`, `mediaTrackEvent`, `mediaUpdatePlayhead` 및 `mediaUpdateQoS`)와 동일한 미디어 메서드를 노출하므로 이벤트 및 변수 페이지에 표시된 호출이 동일한 방식으로 작동합니다. Setter API는 직접 호출됩니다. getter API는 `API_RESPONSE` 콜백을 통해 값을 반환합니다.

## 다음 단계

구현이 완료되면 [Analytics 전용 구현에 대한 보고를 설정](/help/reporting/setup/analytics-reporting.md)할 수 있습니다.

>[!MORELIKETHIS]
>
>* [이벤트 개요](/help/implementation/events/overview.md)
>* [변수 개요](/help/implementation/variables/overview.md)
>* [Roku Edge SDK](/help/implementation/edge/roku.md)
