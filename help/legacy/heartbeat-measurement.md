---
title: 하트비트 측정 정보
description: 하트비트를 사용하여 비디오 지표를 수집하는 방법에 대해 알아봅니다.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
TQID: https://experienceleague.adobe.com/t6Y8Nj7WaEP76UOj8cCp40zSc3mHMfZuC9j5CifVIOg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: eb9732ab-8232-4b21-bc4c-89de86dbe4d7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e6c28e30-8689-4bf4-8fa8-561343d308a9
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 316
ht-degree: 31%

---

# 하트비트 측정 정보

Adobe 스트리밍 미디어 서비스는 &quot;하트비트&quot;를 사용하여 비디오 지표를 수집합니다. 비디오 재생 중에 하트비트가 하트비트 추적 서버로 전송되어 재생 시간이 측정됩니다. 하트비트 호출은 10초마다 전송됩니다. 하트비트는 세부적인 비디오 참여 지표와 보다 정확한 비디오 폴아웃 보고서를 생성합니다. 스트리밍 미디어 서비스는 Media Analytics 확장, Media SDK 및 Media Collection API와 함께 Adobe Launch를 사용하여 하트비트를 측정합니다. `AppMeasurement` 및 `VisitorID` 구성 요소가 비디오 데이터를 받는 데 사용됩니다.

Streaming Media 서비스에서 하트비트를 사용하면 다음과 같은 이점이 있습니다.

| 기능 | 설명 |
|---|---|
| 미디어 이벤트 | 상세하고 사용자 지정된 이벤트가 기본 콘텐츠의 경우 10초마다, 광고의 경우 1초마다 전송됩니다. |
| 지표 및 차원 | 공급업체 간 명확하고 표준화된 지표, 차원 및 벤치마크입니다. 모든 플랫폼에서 표준화된 솔루션을 사용하므로 모든 미디어 및 플랫폼에서 일관적으로 표준화된 변수를 사용하여 보다 효율적인 교차 캠페인, 디바이스 및 공급업체 비교를 허용할 수 있습니다. |
| 통합 | Experience Cloud ID는 보다 쉬운 교차 분석을 위해 Adobe Experience Cloud에 연결됩니다. 자동 Adobe Experience Cloud 통합을 통해 미디어 대상을 세그먼트화하고, 타깃팅하고, 사용자 환경 설정을 기반으로 미디어를 추천할 수 있습니다. |
| 가격 책정 | 미디어 스트림별 투명한 추적(단일) |
| 구현 및 지원 | 지속적인 업데이트 및 개선 사항으로 간소화된 구성 간소화된 구현 프로세스를 사용하므로 플레이어 API를 통해 변수를 빠르게 매핑하고 Adobe 디버그 도구를 사용하여 구현을 확인하여 필요한 모든 변수가 정확하게 추적되도록 합니다. |
| 파트너 공유 | Federated Media 및 인증된 지표. Federated Media를 통해 공유된 데이터를 사용하면 업계 최초 미디어 공유 기능을 통해 모든 미디어 배포 파트너(운영자, 프로그래머 및 배포자)의 데이터를 전체적으로 평가할 수 있습니다. |
| 고급 추적 | 다운로드한 컨텐츠 추적, 오류 복구 추적 및 Concurrent Viewer. 연결에 관계없이 장치에서 다운로드 및 재생되는 스트리밍 미디어 콘텐츠를 추적할 수 있습니다. |
