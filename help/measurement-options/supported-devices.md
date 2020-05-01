---
title: 지원되는 디바이스
description: null
uuid: null
translation-type: tm+mt
source-git-commit: 3a237ee31412784f708e772cc3a58047630e2184

---


# 지원되는 디바이스 {#devices-supported}

오디오 및 비디오용 Adobe Analytics를 사용하면 모든 디바이스에서 각 미디어 스트림을 수집하고 보고할 수 있습니다.

오디오 및 비디오용 Adobe Analytics는 다음을 비롯한 모든 주요 장치를 지원합니다.

* iOS 및 Android 스마트폰 및 태블릿
* ROKU, AppleTV, FireTV 및 Android TV용 OTT 장치
* 데스크톱 및 랩톱용 JavaScript 브라우저

미디어 SDK는 새로운 버전의 디바이스가 출시되면 정기적으로 업데이트되며 SDK를 사용하여 Brightcove 및 Oyala를 비롯한 오늘날 가장 큰 미디어 플레이어와 통합할 수 있습니다.

현재 SDK 지원이 없는 디바이스 또는 플랫폼이나 SDK를 사용하지 않으려는 경우 Media Collection API를 구현할 수 있습니다. Media Collection API를 사용하면 디바이스 또는 플랫폼에서 Media Analytics 백엔드로 바로 RESTful API 호출을 만들 수 있습니다.

아래 표는 현재 지원되는 장치입니다. 최신 버전의 SDK를 다운로드하려면 [SDK 다운로드를 참조하십시오](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/download-sdks.html). 장치가 목록에 없으면 고객 지원 센터 또는 솔루션 컨설턴트에게 해당 장치의 상태를 문의하십시오.


| 스트리밍 플랫폼/디바이스 |  | AEP SDK를 통한 미디어 실행 확장 | Media SDK | Media Collection API |
|---------------------------|-----------------------------------------------|:----------------------------:|:-------------------:|:--------------------:|
| 웹/모바일 웹 |  |  |  |  |
|  | JavaScript 브라우저 | X | X | X |
| 모바일 앱 |  |  |  |  |
|  | iOS 장치 | X | X | X |
|  | Android 장치 | X | X | X |
|  | Windows 장치 |  |  | X |
| OTT |  |  |  |  |
|  | Apple TV(레거시, TVOS) |  | X | X |
|  | ROKU |  | X<br>(BrightScript) | X<br>(기본) |
|  | Fire TV(Fire OS) |  | X | X |
|  | Android TV |  | X | X |
|  | Chromecast |  | X | X |
|  | 게임 콘솔(예: Xbox ONE, Sony PS3/PS4) |  |  | X |
|  | 상위 박스 설정(예: Exfinity X1) |  |  | X |
|  | 스마트 TV(예: 삼성, LG, 소니, 비지오) |  | X<br>(웹 기반) | X |
| 기타 |  |  |  |  |
|  | 새로운 연결된 디바이스 |  |  | X |


Media SDK의 경우 [최소 플랫폼 버전 지원](/help/sdk-implement/setup/setup-overview.md#minimum-platform-version)을 참조하십시오.
