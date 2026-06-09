---
title: 스트리밍 미디어용 Roku Edge 설정
description: 스트리밍 미디어 데이터를 Adobe Experience Platform으로 보내도록 Edge Network Roku SDK을 구성합니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# 스트리밍 미디어용 Roku Edge 설정

[Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku)&#x200B;(BrightScript)가 Roku 채널에서 미디어 세션 데이터를 수집하여 Edge Network으로 보냅니다. Roku는 코드로 구성되어 있으며 태그를 사용하지 않습니다.

* **필수 구성 요소**:
   * [Edge 구현 개요](overview.md)([!UICONTROL Media Analytics]이(가) 활성화된 스키마, 데이터 세트, 데이터 스트림)를 완료합니다.
   * [시작 안내서](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/getting-started.md)에 설명된 대로 [GitHub 릴리스](https://github.com/adobe/aepsdk-roku/releases)에서 SDK을 다운로드하고 채널에 추가합니다.

## 미디어용 Roku Edge SDK 구성

SDK을 초기화하고 데이터 스트림 및 미디어 구성을 설정합니다.

```brightscript
m.aepSdk = AdobeAEPSDKInit()
ADB_CONSTANTS = AdobeAEPSDKConstants()

configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<datastreamID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "sample_channel"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
m.aepSdk.updateConfiguration(configuration)
```

그런 다음 `createMediaSession`(으)로 세션을 엽니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": { "name": "video-123", "length": 128, "contentType": "vod", "streamType": "video" },
            "playhead": 0
        }
    }
})
```

>[!IMPORTANT]
>
>재생 중에 최신 플레이헤드 값으로 초당 한 번 이상 `media.ping` 이벤트를 보냅니다. Roku Edge SDK은 이러한 Ping을 사용하여 올바르게 작동합니다.

구성 키 및 전체 API에 대해서는 [Roku Edge SDK API 참조](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/api-reference.md)를 참조하십시오.

## 미디어 이벤트 추적

세션이 열린 후 `sendMediaEvent`(으)로 각 미디어 이벤트를 보냅니다. 정확한 페이로드는 각 [이벤트](/help/implementation/events/overview.md) 및 [변수](/help/implementation/variables/overview.md) 페이지에서 **Roku Edge** 탭을 참조하십시오.

## 다음 단계

구현이 완료되면 [Edge 구현에 대한 보고를 설정](/help/reporting/setup/edge-reporting.md)할 수 있습니다.

>[!MORELIKETHIS]
>
>* [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku)
>* [이벤트 개요](/help/implementation/events/overview.md)
>* [변수 개요](/help/implementation/variables/overview.md)
