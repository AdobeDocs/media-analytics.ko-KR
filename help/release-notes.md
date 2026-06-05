---
title: 스트리밍 미디어 서비스 릴리스 정보
description: 스트리밍 미디어 서비스에 대한 릴리스 정보를 확인하십시오.
feature: Release Notes
role: User, Admin, Developer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
TQID: https://experienceleague.adobe.com/yNfosiewndKE7c-VjoVM6D3ifYlgX3eJGgYQWcBC9no
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: f73667dc-d296-4875-8975-ac3fdc3adc42
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: ac8a38fa-dec3-4581-8f64-178fde9f64e8
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: 720
ht-degree: 36%

---

# 스트리밍 미디어 서비스 릴리스 정보

**마지막 업데이트**: 2026년 6월 4일

## 2026

| 기능 | 설명 | 날짜 |
| --- | --- | --- |
| **일정 데이터 지원** | 이전 라이브 콘텐츠에 대해 예약된 데이터를 업로드하여 프로그램 또는 세그먼트별로 시청률을 추적합니다. 지원되는 콘텐츠 유형은 다음과 같습니다.<ul><li>FAST(무료 광고 지원 TV) 플랫폼</li><li>로컬 스트림</li><li>라이브 스포츠</li></ul>자세한 내용은 [라이브 콘텐츠를 추적할 일정 데이터 업로드](/help/use-cases/track-schedule-data.md) 사용 사례를 참조하십시오. | 롤아웃 시작: 2025년 10월 29일<p>일반 가용성: 2026년 10월</p> |

## 2025

| 기능 | 설명 | 날짜 |
| --- | --- | --- |
| **`mediaTimed`XDM 필드 사용 중단** | `mediaTimed` XDM 개체는 `mediaReporting` 필드 경로를 위해 더 이상 사용되지 않습니다. 2025년 5월 9일 이전에 Analytics 소스 커넥터를 구현한 고객은 구성을 마이그레이션해야 합니다. 자세한 내용은 다음 마이그레이션 안내서를 참조하십시오.<ul><li>[대상을 새 스트리밍 미디어 필드로 마이그레이션](/help/implementation/edge/migrate/migrate-audiences.md)</li><li>[새 스트리밍 미디어 필드를 사용하도록 Customer Journey Analytics 마이그레이션](/help/implementation/edge/migrate/migrate-cja-setup.md)</li><li>[사용자 지정 필드에 대한 데이터 준비를 새 스트리밍 미디어 필드로 마이그레이션](/help/implementation/edge/migrate/migrate-dataprep.md)</li><li>[프로필을 새 스트리밍 미디어 필드로 마이그레이션](/help/implementation/edge/migrate/migrate-profiles.md)</li></ul> | 2025년 10월 |

## 2024

| 기능 | 설명 | 날짜 |
| --- | --- | --- |
| **웹 SDK 지원** | Web SDK 또는 Web SDK 태그 확장을 사용하여 Adobe Experience Platform Edge Network에 스트리밍 미디어 웹 데이터를 보내어 Customer Journey Analytics, Real-time CDP, Journey Optimizer 및 이벤트 전달과 같은 플랫폼 솔루션에서 통합 수집 방법을 활성화합니다. 자세한 내용은 [스트리밍 미디어용 웹 SDK 설정](/help/implementation/edge/web-sdk.md) 또는 [스트리밍 미디어용 웹 SDK 태그 확장 설정](/help/implementation/edge/web-sdk-tags.md)을 참조하십시오. | 2024년 5월 29일 목요일 |
| **Roku 지원** | Roku SDK을 사용하여 Adobe Experience Platform에 스트리밍 미디어 데이터를 전송합니다. 자세한 내용은 [스트리밍 미디어용 Roku 설정](/help/implementation/edge/roku.md)을 참조하십시오. | 2024년 4월 12일 토요일 |

## 2023

| 기능 | 설명 | 날짜 |
| --- | --- | --- |
| **Experience Edge 지원** | iOS 및 Android용 Media Edge API 또는 Mobile SDK를 사용하여 스트리밍 미디어 컬렉션을 구현합니다.<ul><li>[스트리밍 미디어용 Media Edge API 설정](/help/implementation/edge/media-edge-api.md)</li><li>[스트리밍 미디어용 iOS 설정](/help/implementation/edge/ios.md) 또는 [태그를 사용하는 스트리밍 미디어용 iOS 설정](/help/implementation/edge/ios-tags.md)</li><li>[스트리밍 미디어용 Android 설정](/help/implementation/edge/android.md) 또는 [태그를 사용하는 스트리밍 미디어용 Android 설정](/help/implementation/edge/android-tags.md)</li></ul> | 2023년 5월 12일 토요일 |

## 2022

| 기능 | 설명 | 날짜 |
| --- | --- | --- |
| **여러 플레이어 상태 추적** | 미디어 컬렉션 API를 사용하여 여러 [플레이어 상태 추적](/help/implementation/events/player-state/overview.md)을 구현합니다. | 2022년 9월 |
| 이름이 변경된 XDM 필드 | 일관성을 위해 이름이 변경된 XDM 필드 이름:<ul><li>오디오 및 비디오 매개 변수</li><li>광고 매개변수</li><li>챕터 매개변수</li><li>플레이어 상태 매개변수</li><li>품질 매개변수</li></ul> | 2022년 9월 |
| **Customer Journey Analytics에 패널 추가됨** | [미디어 동시 뷰어 패널](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers) 및 [미디어 재생 소요 시간 패널](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)을 Customer Journey Analytics에 추가했습니다. | 2022년 8월 9일 수요일 |
| **평균 분당 시청 대상자** | [분당 평균 시청 시간 패널](https://experienceleague.adobe.com/ko/docs/analytics/analyze/analysis-workspace/panels/average-minute-audience-panel)을 사용하여 평균 콘텐츠 소비에 대해 더 잘 이해할 수 있습니다. <br>평균 분당 시청자를 통해 모든 길이 또는 모든 장르의 프로그램을 비교할 수 있습니다. 또한 디지털 평균 분당 시청자를 유선 TV 평균 분당 지표와 비교하거나 추가할 수 있습니다. 이 패널을 통해 기간 분류가 업데이트된 경우에도 사용자 정의 기간의 대상자 평균을 보다 유연하게 측정할 수 있습니다. | 2022년 3월 16일 목요일 |

## 2021

| 기능 | 설명 | 날짜 |
| --- | --- | --- |
| **미디어 재생 소요 시간** | [재생 소요 시간 패널](https://experienceleague.adobe.com/ko/docs/analytics/analyze/analysis-workspace/panels/media-playback-time-spent)은 시청자 참여에 대한 가치 있는 insight을 제공하며 미디어 조직에서는 시간대 지정 기능이 있는 고급 소요 시간 분석을 통해 분 단위 사용자 참여에 대한 보다 심층적이고 세부적인 통찰력을 얻을 수 있습니다. 특정 시점에 미디어 스트림을 보는 데 소요된 시간을 관찰할 수 있습니다. 새로운 5분, 15분, 30분 단위를 포함하여 다양한 단위로 재생 시간을 분할할 수 있습니다. | 2021년 9월 |

## 2020

| 기능 | 설명 | 날짜 |
| --- | --- | --- |
| **미디어 동시 뷰어 패널** | [동시 뷰어 패널](https://experienceleague.adobe.com/ko/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers)을 통해 최대 동시 시청 횟수가 발생한 위치 또는 드롭오프가 발생한 위치를 파악할 수 있습니다. 콘텐츠 및 뷰어 참여의 품질에 대한 중요한 인사이트를 얻고 볼륨 및 규모에 대한 문제 해결 또는 계획을 수립하는 데 도움이 됩니다.<br><br>[미디어 동시 뷰어 패널(튜토리얼)](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace) | 2020년 9월, 2021년 1월 |
| **지원되는 디바이스 및 플랫폼** | 이제 AEP SDK가 포함된 미디어 실행 확장자는 다음과 같은 OTT 디바이스를 지원합니다. <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul></div> | 2020년 6월 |
