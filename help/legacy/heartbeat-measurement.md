---
title: 하트비트 측정 정보
description: 하트비트를 사용하여 비디오 지표를 수집하는 방법에 대해 알아봅니다.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 86%

---

# 하트비트 측정 정보

Adobe 스트리밍 미디어 컬렉션 추가 기능은 &quot;하트비트&quot;를 사용하여 비디오 지표를 수집합니다. 비디오 재생 중에 하트비트가 하트비트 추적 서버로 전송되어 재생 시간이 측정됩니다. 하트비트 호출은 10초마다 전송됩니다. 하트비트는 세부적인 비디오 참여 지표와 보다 정확한 비디오 폴아웃 보고서를 생성합니다. Streaming Media는 Media Analytics 확장, Media SDK 및 Media Collection API와 함께 Adobe Launch를 사용하여 하트비트를 측정합니다. `AppMeasurement` 및 `VisitorID` 구성 요소가 비디오 데이터를 받는 데 사용됩니다.

Streaming Media Collection 추가 기능에서 하트비트를 사용하면 다음과 같은 이점이 있습니다.

| 기능 | 설명 |
|---|---|
| 미디어 이벤트 | 상세하고 사용자 지정된 이벤트가 기본 콘텐츠의 경우 10초마다, 광고의 경우 1초마다 전송됩니다. |
| 지표 및 차원 | 공급업체 간 명확하고 표준화된 지표, 차원 및 벤치마크모든 플랫폼에서 표준화된 솔루션을 사용합니다. 모든 미디어 및 플랫폼에서 일관적으로 표준화된 변수를 사용하여 보다 효율적인 교차 캠페인, 디바이스 및 공급업체 비교를 허용할 수 있습니다. |
| 통합 | Experience Cloud ID가 보다 쉬운 교차 분석을 위해 Adobe Experience Cloud에 연결되어 있음. 자동 Adobe Experience Cloud 통합을 사용하므로 미디어 대상자를 세그먼트화하고, 타겟팅하고, 사용자 환경 설정을 기반으로 미디어를 추천할 수 있습니다. |
| 가격 책정 | 미디어 스트림별 투명한 추적(단일) |
| 구현 및 지원 | 지속적인 업데이트 및 개선 사항으로 간소화된 구성. 간소화된 구현 프로세스를 사용하므로 플레이어 API를 통해 변수를 빨리 매핑하고 Adobe Debug 도구를 통해 구현을 확인하여 필요한 모든 변수가 정확하게 추적되도록 합니다. |
| 파트너 공유 | Federated Analytics 및 인증된 지표. Federated Analytics를 통해 공유된 데이터를 사용하므로 업계 최초 미디어 공유 기능을 통해 모든 미디어 배포 파트너(운영자, 프로그래머 및 배포자)의 데이터를 전체적으로 평가할 수 있습니다. |
| 고급 추적 | 다운로드한 콘텐츠 추적, 오류 복구 추적 및 Concurrent Viewer. 연결 여부에 관계없이 디바이스에서 다운로드 및 재생되는 Streaming Media 콘텐츠를 추적할 수 있습니다. |
