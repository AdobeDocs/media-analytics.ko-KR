---
title: 스트리밍 미디어용 iOS 설정
description: iOS에서 Adobe Experience Platform Mobile SDK을 구성하여 스트리밍 미디어 데이터를 Edge Network으로 보냅니다.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 스트리밍 미디어용 iOS 설정

Adobe Streaming Media for Edge Network 확장(`AEPEdgeMedia`)은 iOS 또는 tvOS 앱에서 미디어 세션 데이터를 수집하여 Edge Network으로 보냅니다. 이 페이지에서는 코드 내 구성에 대해 설명합니다. 대신 Tags 모바일 속성을 통해 SDK을 구성하려면 [Tags를 사용하는 스트리밍 미디어용 iOS 설정](ios-tags.md)을 참조하십시오.

* **필수 구성 요소**:
   * [Edge 구현 개요](overview.md)([!UICONTROL Media Analytics]이(가) 활성화된 스키마, 데이터 세트, 데이터 스트림)를 완료합니다.
   * `AEPCore`, `AEPEdge`, `AEPEdgeIdentity` 및 `AEPEdgeMedia` 확장을 앱에 추가합니다. 설치 및 등록은 [Edge Network용 Adobe 스트리밍 미디어](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)를 참조하십시오.

## iOS용 미디어 구성

SDK을 초기화할 때 미디어 구성 키를 설정합니다.

```swift
let configuration = [
  "edgeMedia.channel": "sample_channel",
  "edgeMedia.playerName": "player_name",
  "edgeMedia.appVersion": "app_version"
]
MobileCore.updateConfiguration(configuration)
```

그런 다음 추적기를 만들어 미디어 세션을 관리합니다.

```swift
let tracker = Media.createTracker()
```

구성 키 및 전체 추적기 API에 대해서는 [Edge Network API용 Media 참조](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/api-reference/)를 참조하십시오.

## 미디어 이벤트 추적

추적기가 만들어진 상태에서 추적기 메서드를 사용하여 각 미디어 이벤트를 추적합니다. 정확한 호출은 각 [이벤트](/help/implementation/events/overview.md) 및 [변수](/help/implementation/variables/overview.md) 페이지에서 **iOS** 탭을 참조하십시오.

## 다음 단계

구현이 완료되면 [Edge 구현에 대한 보고를 설정](/help/reporting/setup/edge-reporting.md)할 수 있습니다.

>[!MORELIKETHIS]
>
>* [Edge Network용 Adobe 스트리밍 미디어](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [태그가 있는 스트리밍 미디어용 iOS 설정](ios-tags.md)
>* [이벤트 개요](/help/implementation/events/overview.md)
