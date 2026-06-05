---
title: Media SDK, 확장 프로그램 및 API 가져오기
description: Android, iOS, JavaScript, Chromecast 및 Roku를 비롯한 사용 가능한 플랫폼에 대한 SDK 다운로드 링크입니다.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/-L2tSDNue-GheYE-krKkpnOh05s5GKZZBz5sFXsBJ3I
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c77ba355-6681-41fe-b719-563d3f507fdbid: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: b18eab3deb3d15a08adf2f7ecf61d73235bbc6e5
workflow-type: tm+mt
source-wordcount: 575
ht-degree: 32%

---

# Media SDK, 확장 프로그램 및 API 가져오기

## Edge 구현(권장) {#edge-sdks}

Edge 구현은 데이터를 한 번 수집하고 Adobe Experience Platform Edge Network을 통해 Adobe Analytics, Customer Journey Analytics, Adobe Journey Optimizer 및 Real-Time CDP과 같은 여러 대상으로 전달합니다. 기본 SDK이 없는 플랫폼(예: 스마트 TV, 게임 콘솔 및 셋톱 박스)의 경우 Media Edge API를 사용하십시오.

| | 설명서 | 샘플 |
|:---:|---|---|
| [![JavaScript 아이콘](assets/javascript-icon.png)](https://experienceleague.adobe.com/ko/docs/experience-platform/web-sdk/install/overview)<br>[웹 SDK](https://experienceleague.adobe.com/ko/docs/experience-platform/web-sdk/install/overview) | [스트리밍 미디어용 웹 SDK 설정](/help/implementation/edge/web-sdk.md) | [샘플](https://github.com/adobe/alloy-samples/blob/main/media-collection/STANDALONE.md) |
| [![확장 아이콘](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html)<br>[웹 SDK 태그 확장](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html) | [스트리밍 미디어용 웹 SDK 태그 확장 설정](/help/implementation/edge/web-sdk-tags.md) | [샘플](https://github.com/adobe/alloy-samples/blob/main/media-collection/TAGS_IMPL.md) |
| [![Android 아이콘](assets/android.png)](https://github.com/adobe/aepsdk-media-android)<br>[Android SDK](https://github.com/adobe/aepsdk-media-android) | [스트리밍 미디어용 Android 설정](/help/implementation/edge/android.md) | [샘플](https://github.com/adobe/aepsdk-media-android/tree/main/code/testapp) |
| [![Apple iOS 아이콘](assets/apple.png)](https://github.com/adobe/aepsdk-media-ios)<br>[iOS/tvOS SDK](https://github.com/adobe/aepsdk-media-ios) | [스트리밍 미디어용 iOS 설정](/help/implementation/edge/ios.md) | [샘플](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| [![확장 아이콘](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[Android 태그 확장](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [스트리밍 미디어용 Android 태그 확장 설정](/help/implementation/edge/android-tags.md) | |
| [![확장 아이콘](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[iOS/tvOS 태그 확장](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [스트리밍 미디어용 iOS 태그 확장 설정](/help/implementation/edge/ios-tags.md) | |
| [![Roku 아이콘](assets/roku-icon.png)](https://github.com/adobe/aepsdk-roku)<br>[Roku SDK](https://github.com/adobe/aepsdk-roku) | [스트리밍 미디어용 Roku 설정](/help/implementation/edge/roku.md) | [샘플](https://github.com/adobe/aepsdk-roku/tree/main/sample/simple-videoplayer-channel) |
| [![API 아이콘](assets/api.png)](https://developer.adobe.com/data-collection-apis/docs/api/media-edge)<br>[미디어 Edge API](https://developer.adobe.com/data-collection-apis/docs/api/media-edge) | [Media Edge API 설정](/help/implementation/edge/media-edge-api.md) | [샘플](https://developer.adobe.com/data-collection-apis/docs/getting-started/media-edge-examples) |

## Analytics 전용 구현 {#analytics-only-sdks}

이러한 SDK 및 확장은 데이터를 Adobe Analytics으로 직접 전송합니다. 새로운 구현의 경우 위의 Edge 구현을 사용하십시오. 기존 Analytics 데이터를 Customer Journey Analytics 또는 다른 Experience Platform 애플리케이션으로 가져오려면 [Analytics 소스 커넥터](https://experienceleague.adobe.com/ko/docs/experience-platform/sources/connectors/adobe-applications/analytics)를 사용하십시오.

| | 설명서 | 샘플 |
|:---:|---|---|
| [![JavaScript 아이콘](assets/javascript-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2)<br>[미디어 SDK 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [스트리밍 미디어용 JavaScript 설정](/help/implementation/analytics-only/javascript.md) | [샘플](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| [![확장 아이콘](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=ko)<br>[미디어 확장](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=ko) | [스트리밍 미디어용 태그를 사용하여 JavaScript 설정](/help/implementation/analytics-only/javascript-tags.md) | [샘플](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| [![Chromecast 아이콘](assets/chromecast-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3)<br>[Chromecast SDK 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [스트리밍 미디어용 Chromecast 설정](/help/implementation/analytics-only/chromecast.md) | [샘플](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/chromecast/samples/BasicPlayerSample) |
| [![API 아이콘](assets/api.png)](/help/implementation/media-collection-api/mc-api-overview.md)<br>[미디어 컬렉션 API](/help/implementation/media-collection-api/mc-api-overview.md) | [미디어 컬렉션 API 설정](/help/implementation/analytics-only/media-collection-api.md) | |
