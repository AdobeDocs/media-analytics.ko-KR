---
title: 스트리밍 미디어용 웹 SDK 설정
description: Adobe Experience Platform 웹 SDK(alloy.js)를 구성하여 스트리밍 미디어 데이터를 Edge Network으로 보냅니다.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 5%

---

# 스트리밍 미디어용 웹 SDK 설정

Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/js-overview)&#x200B;(`alloy.js`, 버전 2.20.0 이상)의 `streamingMedia` 구성 요소는 웹 사이트에서 미디어 세션 데이터를 수집하여 Edge Network으로 보냅니다. 이 페이지에서는 코드 내(`alloy.js`) 구성에 대해 설명합니다. 대신 태그를 통해 웹 SDK을 구성하려면 [스트리밍 미디어용 웹 SDK 태그 확장 설정](web-sdk-tags.md)을 참조하십시오.

* **필수 구성 요소**:
   * [Edge 구현 개요](overview.md)([!UICONTROL Media Analytics]이(가) 활성화된 스키마, 데이터 세트, 데이터 스트림)를 완료합니다.
   * 웹 SDK 2.20.0 이상을 설치합니다. [웹 SDK 설치](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/install/overview)를 참조하십시오.

## streamingMedia 구성 요소 구성

`alloy` 구성에 `streamingMedia` 구성 요소 추가:

```js
alloy("configure", {
  edgeConfigId: "<datastreamID>",
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

전체 구성에 대한 자세한 내용은 [`streamingMedia` 명령](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/streamingmedia)을(를) 참조하십시오.

### Media JS SDK에서 마이그레이션

Media JS(3.x) SDK에서 이동하는 경우 웹 SDK [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/getmediaanalyticstracker) 명령은 [3.x Media SDK](/help/implementation/analytics-only/javascript.md)과(와) 동일한 API를 노출하는 추적기 인스턴스를 반환하므로 기존 추적 호출이 계속 작동합니다.

## 미디어 이벤트 추적

SDK이 구성된 상태에서 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출하여 각 미디어 이벤트를 보냅니다. 정확한 페이로드는 각 [이벤트](/help/implementation/events/overview.md) 및 [변수](/help/implementation/variables/overview.md) 페이지에서 **웹 SDK** 탭을 참조하십시오.

## 다음 단계

구현이 완료되면 [Edge 구현에 대한 보고를 설정](/help/reporting/setup/edge-reporting.md)할 수 있습니다.

>[!MORELIKETHIS]
>
>* [Web SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/js-overview)
>* [이벤트 개요](/help/implementation/events/overview.md)
>* [변수 개요](/help/implementation/variables/overview.md)
