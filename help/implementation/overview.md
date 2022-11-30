---
title: Adobe Analytics용 스트리밍 미디어 구현
description: 스트리밍 미디어 구현 경로에 대해 자세히 알아봅니다.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: a7d897c6f6fbc6ed0d5b71f5801ab18ee21f0411
workflow-type: ht
source-wordcount: '138'
ht-degree: 100%

---

# Adobe Analytics용 스트리밍 미디어 구현

구현 경로는 Media SDK의 기본 제공 로직(표준, 권장 구현)을 사용할지 또는 직접 롤하여 간단하지만 강력하고 사용자 정의 가능한 Media Collection API(RESTful)를 사용할지 여부에 따라 달라집니다.

지원되는 플랫폼에 따라 구현 경로를 선택하십시오. 일부 플레이어는 Media SDK 또는 Adobe Experience Platform Media SDK에서 지원되지 않으며 Media Collection API는 해당 플레이어를 지원하는 방법을 제공합니다. 지원되는 디바이스에 대한 자세한 내용은 [지원되는 디바이스 및 플랫폼](/help/getting-started/supported-devices.md)을 참조하십시오.

![미디어 흐름](media-sdk/assets/choose-media-flow2.png)

Media SDK 및 확장 기능 다운로드 및 설치에 대한 자세한 내용은 [Media SDK, 태그를 사용한 확장 기능 및 OTT SDK 가져오기](/help/getting-started/download-sdks.md)를 참조하십시오.

Media Collection API 사용에 대한 자세한 내용은 [Media Collection API](media-collection-api/mc-api-overview.md)를 참조하십시오.