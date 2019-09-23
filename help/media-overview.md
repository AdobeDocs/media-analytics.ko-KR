---
seo-title: Adobe Analytics에서 오디오 및 비디오 측정
title: Adobe Analytics에서 오디오 및 비디오 측정
uuid: b3cbe240-b94d-42b8-a99c-028033aaa14
translation-type: tm+mt
source-git-commit: 9b6e61e8d97ca44772f5dc2e31472a4f6c54e29c

---


# Adobe Analytics에서 오디오 및 비디오 측정{#measuring-audio-and-video-in-adobe-analytics}

![배너](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>The documentation provided here is specific to clients utilizing version 1.5 or higher of Adobe's *Media SDK* for heartbeat measurement, or Adobe's newer *Media Collection API* for heartbeat measurement. 기존 이정표 비디오 구현에 대한 지침은 포함되지 않습니다. 모든 고객이 개선 사항 및 확장된 측정 기능을 활용할 수 있도록 두 개의 최신 미디어 추적 솔루션 중 하나 또는 둘 다 채택할 것을 권장합니다. 아래에서 [최신 솔루션으로 전환했을 때 이점](media-overview.md#section_cnj_5st_p1b)을 확인할 수 있습니다. Adobe는 이정표 비디오 추적 방법을 계속 지원할 예정이지만 계획된 업데이트, 수정 사항 또는 기능 개선 사항은 없습니다. 추가 질문이 있는 경우 Adobe 계정 관리자에게 문의하십시오.

## 개요 {#section_8BFE4F8DA64B4A5F826A4940B11AA466}

Adobe Analytics for Media(Media Analytics라고도 함)는 고객에게 컨텐츠, 오디오 및 광고에 대한 강력한 미디어 측정 기능을 제공하는 기본 Analytics 서비스의 추가 기능입니다. Media Analytics는 실시간 모니터링, 세부 분석, 조치 가능한 통찰력 및 수익 창출 기회를 얻을 수 있도록 고객에게 많은 이점을 제공합니다.

미디어 추적은 다음 중 하나를 통해 사용할 수 있습니다.

* **Media SDK -** 가장 일반적으로 사용되는 미디어 플레이어와 통합됩니다.
* **Media Collection API -**(RESTful API) SDK 지원이 없는 플레이어(또는 SDK 통합이 필요하지 않은 플레이어)와 통합됩니다.

   Media Collection API는 SDK에서 아직 사용할 수 없는 추가적인 기능도 제공합니다.

   * **다운로드 컨텐츠 추적 -** 연결에 관계없이 장치에서 다운로드 및 재생되는 미디어 컨텐츠 추적(비디오 및 오디오)에 대한 지원을 제공합니다. 이 기능은 Media Collection API 위에 구축되며 동일한 플레이어 추적 사양을 따릅니다. (현재 SDK 지원은 없습니다.)

Adobe Analytics for Media를 사용하면 고객이 해당 사이트에서 미디어 사용을 포함하는 전체 고객 여정을 추적할 수 있으며, 이러한 측정 기능은 쉽게 Analytics 보고 및 기타 Experience Cloud 제품에 통합되어 있습니다. 미디어 측정을 사용하여 데이터를 여러 차원 및 세그먼트로 나누고 분류하여 세부 분석을 수행하는 데 필요한 모든 메타데이터를 캡처할 수 있고, 끝까지 소비한 미디어에 대한 성공 기준, 평균 소요 시간 및 완료된 광고를 표시할 수 있습니다.

미디어 솔루션은 프레임, 버퍼링 시간 및 평균 비트율과 같이 QoS와 관련된 중요한 게재 지표만 측정하지 않습니다. 이 솔루션은 웹 사이트나 앱 데이터와 결합하여 고객 및 고객 관심 사항의 흐름을 시각화하고, 더 나은 추천을 수행하고, Adobe Experience Cloud를 통해 환경을 개인화할 수도 있습니다.

## 이점 {#section_7712BA90EAE64C118218D1C581EF68B7}

Adobe의 미디어 측정 솔루션에서 제공하는 여러 이점 중 몇 가지는 다음과 같습니다.

* **시기 적절한 분석 -** 여러 채널에서 주요 성능 지표(예: 지속 기간)를 활용하여 실시간으로 실행 가능한 결정을 내릴 수 있습니다. 기본 컨텐츠 이벤트는 **10초** 간격으로 측정되어 발생하는 모든 활동을 캡처합니다. 광고 추적 이벤트는 **1초** 간격으로 발생합니다.
* **참여 유도 -** 버퍼링 이벤트 수를 최소화하고, 컨텐츠 내에서 광고를 재생할 위치와 시점을 파악하여 사용자 참여를 유도함으로써 사용자를 다시 불러오고 재방문을 제공하는 유연하고 간단한 경험을 제공합니다.
* **전체적인 화질 - 모든 컨텐츠 배포업체 간의 여러 데이터 포인트를 통합하여 모든 미디어 활동을 전체적으로 파악할 수 있고 Federated Analytics** 기능을 통해 모든 채널에서 참여도 및 보기/청취를 측정할 수 [있습니다](data-sharing/federated-analytics.md) .
* **증가된 세분기간 -** 개별 방문자 시간, 분별 Concurrent Viewer/Listener 및 컨텐츠를 소비한 평균 시간을 포함하여 가장 세분화된 수준에서 보기 동작을 평가합니다.
* **정확한 측정 -** OTT, 스마트폰, 태블릿, 데스크탑 등을 포함하여 미디어 이용에 사용된 여러 장치를 측정하여 사용자 참여 패턴 및 습관을 모니터링합니다.
* **세그멘테이션 -** 플레이어, 장치, 장르, 챕터 및 프로그램에 분류를 적용하여 각 내용이 전체 보기/듣기 및 컨텐츠, 오디오, 광고 및 결합에 대한 고객 참여에 미치는 영향을 확인합니다.

## 하트비트와 이정표의 이점 {#section_cnj_5st_p1b}

Adobe Analytics for Media는 다음 두 가지 방법을 통해 측정할 수 있습니다.기존 이정표 방법(비디오만 해당) 및 현재 하트비트 메서드(미디어 SDK와 미디어 컬렉션 API 모두에 포함되어 있는 오디오 및 비디오) 하트비트 메서드는 기본 측정 메서드이므로, 모든 클라이언트가 아래에 설명된 이점을 이용할 수 있도록 이 버전으로 이동할 것을 권장합니다(이 버전이 아직 없는 경우).

기존 이정표 메서드는 비디오 시작, 사분위수 이동, 길이 및 완료에 대해 Analytics Server에 대한 개별 서버 호출을 기반으로 합니다. 하트비트 메서드는 발전되고 표준화된 지표를 제공하기 위해 10초 간격으로 기본 컨텐츠를 측정하는 강력한 미디어 추적 솔루션을 제공합니다. 또한 Adobe는 하트비트가 활용하는 Media SDK 또는 Media Collection API를 통해 더 유연하고 능률적인 구현 프로세스를 제공하기 위해 이정표 메서드에서 학습을 추출했습니다.

하트비트 메서드의 여러 이점 중 몇 가지는 다음과 같습니다.

* **간소화된 구현 프로세스 -** 플레이어 API를 통해 변수를 쉽게 매핑하고 Adobe Debug 도구를 통해 구현을 확인하여 필요한 모든 변수가 정확하게 추적되도록 합니다.
* **자동 Adobe Experience Cloud 통합 -** Experience Cloud ID를 통하여 Adobe Experience Cloud와 자동으로 통합하고, 미디어 대상을 세그먼트화하고, 타깃팅하고, 사용자 환경 설정을 기반으로 미디어를 추천할 수 있습니다.
* **Federated Analytics를 통해 공유된 데이터 -** 업계 최초 미디어 공유 기능을 통해 모든 미디어 배포 파트너(운영자, 프로그래머 및 배포자)의 데이터를 전체적으로 평가할 수 있습니다.
* **인증된 등급의 파트너와 파트너 관계 -** Adobe는 대상 등급 파트너 Nielsen과 협력하여 신뢰할 수 있고 인증된 등급을 허용하도록 중립적인 타사 측정 기능을 제공합니다.
* **모든 플랫폼에서 표준화된 솔루션 -** 모든 미디어 및 플랫폼에서 일관적으로 표준화된 변수를 사용하여 보다 효율적인 교차 캠페인, 장치 및 공급업체 비교를 허용합니다.

### 비교 차트

|  | 비디오 분석 이정표 | Media Analytics - 하트비트 |
|---|---|---|
| **미디어 이벤트** | 상위 수준의 표준 이벤트 | 기본 컨텐츠의 경우 10초마다, 광고의 경우 1초마다 세부 및 사용자 지정 이벤트 발생 |
| **지표 및 차원** | 공급업체, 비표준 지표 및 차원의 차이 | 공급업체 간의 표준화된 명확한 지표, 차원 및 벤치마크 |
| **Adobe 제품과 통합** | 일부 매핑 및 통합을 사용한 개별 세션 | 쉽게 교차 분석할 수 있도록 결합된 Experience Cloud ID가 Adobe Experience Cloud에 연결됨 |
| **가격 책정** | 각 서버 호출에 대해 추적 및 청구됨 | 미디어 스트림별 투명한 추적(단일) |
| **구현 및 지원** | 기존 버전에 대한 제한된 지원과 업그레이드가 없는 장기 통합 | 진행 중인 업데이트 및 개선 사항으로 간소화된 구성 |
| **파트너 공유** | 해당 없음 | 페더레이션 분석 및 인증된 지표 |
| **고급 추적** | 해당 없음 | 오류 복구 추적 및 Concurrent Viewer |

## 지원 장치 {#section_lkm_l5t_p1b}

Adobe Analytics for Media는 의미 있는 장치에서 각 미디어 스트림을 수집하고 보고하는 강력한 데이터 수집 도구를 제공하기 위해 산업과 함께 발전했습니다. Media SDK는 다음을 포함하여 가장 많이 사용되는 장치용으로 개발되었습니다.

* iOS 및 Android 스마트폰 및 태블릿
* ROKU, AppleTV, FireTV 및 Android TV용 OTT 장치
* 데스크톱 및 랩톱용 JavaScript 브라우저

SDK는 새 버전의 장치가 출시될 때 관례적으로 업데이트되므로, 이러한 SDK를 사용하여 Brightcove 및 Ooyala와 같은 가장 큰 대부분의 미디어 플레이어와 통합할 수 있습니다.

현재 SDK를 지원하지 않는 장치나 플랫폼의 경우(또는 이들이 수행하는 경우라도) 장치/플랫폼에서 Media Analytics 백엔드로 직접 RESTful API를 호출하여 Media Collection API를 구현할 수 있습니다.

아래 표는 Media SDK 구현 및 Media Collection API 구현을 통해 현재 지원되는 장치 목록을 제공합니다. 최신 버전의 SDK를 다운로드하려면 [SDK 다운로드를 참조하십시오.](sdk-implement/download-sdks.md) 측정값을 찾는 장치가 나열되어 있지 않은 경우, 고객 지원 또는 솔루션 컨설턴트에게 해당 장치의 상태에 대해 문의하십시오.

|      | Media SDK | Media Collection API |
|---|:---:|:---:|
| **JavaScript 브라우저** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **iOS 장치** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android 장치** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **통합 Windows 플랫폼(UWP)** |  | ![](assets/icon-blue-check.png) |
| **Blackberry** |  | ![](assets/icon-blue-check.png) |
| **Apple TV(신규/기존)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU(JS)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU(기본 앱)** |  | ![](assets/icon-blue-check.png) |
| **OSX** |  | ![](assets/icon-blue-check.png) |
| **Fire TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Chromecast** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Xbox One/360** |  | ![](assets/icon-blue-check.png) |
| **Sony PS3/PS4** |  | ![](assets/icon-blue-check.png) |
| **(기타/신규 연결된 장치)** |  | ![](assets/icon-blue-check.png) |

미디어 SDK의 경우 최소 [플랫폼 버전 지원을 참조하십시오.](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## 전송 레이어 보안 {#transport-layer-security}

**TLS 알림 —** Adobe는 이전 보안 프로토콜의 사용이 종료되어야 하는 보안 규정 준수 표준을 가지고 있습니다. 지속적으로 발전하는 보안 프로토콜 표준을 준수하기 위해 Adobe는 최신 보안 버전을 사용하기 위해 TLS 1.2를 사용하도록 노력하고 있습니다. 2019년 2월 20일부터 Adobe는 TLS 1.1 이상만 지원합니다. 이러한 변경 사항으로 인해 Adobe는 더 이상 TLS 1.0을 배포하는 이전 디바이스 또는 웹 브라우저에서 최종 사용자의 데이터를 수집하지 않습니다.TLS 1.2로 마이그레이션하면 보안이 개선됩니다. 세부 사항을 살펴보고 원활한 전환을 위한 변경을 계획하는 것이 중요합니다.

>[!NOTE]
>
>TLS는 현재 웹 브라우저와 네트워크를 통해 안전하게 데이터를 교환해야 하는 기타 애플리케이션에서 사용되는 가장 널리 배포된 보안 프로토콜입니다.
