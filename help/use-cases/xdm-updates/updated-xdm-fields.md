---
title: Analytics 소스 커넥터 구현을 스트리밍 미디어 서비스를 위한 새 XDM 필드로 업데이트
description: Analytics 소스 커넥터 구현을 업데이트된 XDM 스트리밍 미디어 필드로 마이그레이션하는 방법에 대해 알아봅니다
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: d239b203-71ce-4307-884f-9d11cc623d04
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# Analytics 소스 커넥터 구현을 스트리밍 미디어 서비스를 위한 새 XDM 필드로 업데이트

>[!NOTE]
>
>이 정보는 [Analytics 소스 커넥터](https://experienceleague.adobe.com/ko/docs/experience-platform/sources/connectors/adobe-applications/analytics)를 사용하여 Adobe Analytics 보고 또는 다른 Platform 서비스와 함께 사용할 수 있도록 스트리밍 미디어 데이터를 Customer Journey Analytics에서 Adobe Experience Platform으로 가져오는 조직을 위한 것입니다.
>
>변경 사항은 데이터 수집, 처리 및 보고를 포함하여 독립형 애플리케이션으로서의 Adobe Analytics에 영향을 주지 않습니다. 데이터 피드 및 처리 규칙과 같은 도구는 영향을 받지 않으므로 Analytics 구현을 업데이트할 필요가 없습니다.

한 XDM 필드 세트에서 다른 XDM 필드로 마이그레이션하는 스트리밍 미디어 서비스를 위한 새로운 Adobe 데이터 수집(Analytics 소스 커넥터) 구현을 이제 사용할 수 있습니다.

## 새 XDM 필드 패스

이 마이그레이션의 일부로 Adobe 데이터 수집(Analytics 소스 커넥터) 흐름에 사용된 XDM 스키마에 `mediaReporting` XDM 필드 경로가 추가되었습니다. 기존 데이터 수집 스키마 및 새로 생성된 모든 Adobe 데이터 수집 스키마에는 이 새 필드가 자동으로 포함됩니다.

## 이전 XDM 필드 패스 대체

스트리밍 미디어 데이터를 Adobe Analytics에서 Adobe Experience Platform으로 전송하는 모든 Adobe 데이터 수집(Analytics 소스 커넥터) 흐름이 현재 새 `mediaReporting` XDM 필드 경로와 이전 `media.mediaTimed` XDM 필드 경로 모두에서 데이터를 전송 중입니다. 이러한 두 필드 경로는 2025년 10월 말까지 3개월 동안 사용할 수 있습니다. 10월 이후에는 `media.mediaTimed` 필드가 완전히 더 이상 사용되지 않으며, 10월 이후에 수집된 데이터에는 `mediaReporting`만 포함됩니다. 사용 중단 후 `media.mediaTimed` 필드가 더 이상 Adobe Experience Platform 스키마 UI에 표시되지 않으며 해당 필드의 데이터 수집이 중지됩니다. 따라서 이러한 필드는 더 이상 Adobe Experience Platform 서비스에서 사용할 수 없습니다.

이 날짜 이전에 수집된 데이터는 보고에 사용할 수 있습니다.

## 새로운 XDM 필드 경로와의 추가적인 차이점

스트리밍 미디어용 새로운 Adobe 소스 커넥터 구현을 통해 Adobe Analytics의 keep-alive 호출이 이제 Adobe Experience Platform으로 수집됩니다.

이전에는 이러한 호출이 Customer Journey Analytics과 같은 플랫폼 앱에 반영되지 않았습니다. 그 결과, 조직에서 다음과 같은 보고 차이점을 관찰할 수 있습니다.

* **정확한 세션 수**: Keep-Alive 호출은 직접 미디어 상호 작용이 없는 경우에도 활성 사용자 세션을 유지 관리하는 데 도움이 되므로 경우에 따라 세션 수의 감소가 발생할 수 있습니다. 이러한 keep-alive 호출은 방문을 열어 두기 위해 미디어 재생당 마지막 이벤트 후 20분마다 생성됩니다. Customer Journey Analytics에서 최적의 세션 추적을 보장하려면 데이터 보기에서 방문 만료를 30분으로 구성하는 것이 좋습니다.

* **이벤트 수가 증가했습니다**: 이제 keep-alive 호출이 Customer Journey Analytics 이벤트 지표에서 계산되기 때문입니다. Keep-alive 호출을 보고에서 제외하려면 이벤트 유형이 `media.keepalive`인 이벤트를 제외하는 필터를 만들 수 있습니다.

이러한 변경 사항으로 Analytics와 CJA 보고 간의 정렬이 향상됩니다.

## 기존 설정 마이그레이션

원활한 전환을 위해 모든 고객은 2025년 10월 말 이전에 기존 설정을 `media.mediaTimed` 필드에서 `mediaReporting` 필드로 마이그레이션해야 합니다. 영향을 받는 영역은 `media.mediaTimed` 사용에 의존하는 영역이며 다음 섹션에 설명된 대로 마이그레이션해야 합니다.

### Customer Journey Analytics**

CJA 보고서를 마이그레이션할 수 있는 방법에는 두 가지가 있습니다.

>[!NOTE]
>
>다음 옵션 중 하나를 선택한 후 Customer Journey Analytics 보고서에 사용된 각 `media.mediaTimed` 필드를 해당 파생 필드 또는 보고 XDM 필드 경로로 수동으로 바꾸어야 합니다.

* **이전 데이터를 유지하려면**: Adobe 팀은 이전 XDM 필드와 새 XDM 필드를 단일 필드로 결합하는 파생 필드 집합을 소개하는 사전 정의된 Customer Journey Analytics 템플릿을 개발했습니다. 이 템플릿은 요청 시 Customer Journey Analytics 연결별로 활성화할 수 있습니다. 새 필드를 활성화하려면 Adobe 지원 팀에 문의하십시오. 이러한 파생된 필드는 조직의 파생된 필드 제한에 포함되지 않습니다.

  매핑 목록을 보려면 [Adobe Experience Platform 및 Customer Journey Analytics에 대한 Media Analytics 매개 변수 매핑](/help/use-cases/xdm-updates/parameters-mapping.md)을 참조하십시오.

* **이전 데이터가 필요하지 않은 경우**: 보고 시 보고 XDM 필드 경로를 사용하면 충분합니다. 자세한 내용은 [새 스트리밍 미디어 필드를 사용하도록 Customer Journey Analytics 마이그레이션](/help/use-cases/xdm-updates/migrate-cja-setup.md)을 참조하십시오.

### Real-Time CDP

모든 대상 및 프로필은 `mediaReporting`을(를) 기반으로 해야 합니다. 자세한 내용은 [새 스트리밍 미디어 필드로 프로필 마이그레이션](/help/use-cases/xdm-updates/migrate-profiles.md)을 참조하십시오.

### 데이터 스트림 및 데이터 수집

동적 구성 및 데이터 매핑은 `mediaReporting`을(를) 사용해야 합니다. 자세한 내용은 [사용자 지정 필드에 대한 데이터 준비를 새 스트리밍 미디어 필드로 마이그레이션](/help/use-cases/xdm-updates/migrate-dataprep.md)을 참조하십시오.

### 마이그레이션해야 하는 기타 서비스

* Adobe Journey Optimizer: 캠페인 및 여정 구성은 `mediaReporting`을(를) 통합해야 합니다.

* 이벤트 전달: 구성에 `mediaReporting` 필드만 포함되어야 합니다.

* Query Services: 쿼리는 `mediaReporting` 필드를 참조해야 합니다.

* 태그 구성: 모든 태그 지정 설정은 `mediaReporting` 필드를 참조해야 합니다.

* 연결 및 대상: 데이터 가져오기 및 내보내기 데이터 흐름은 `mediaReporting` 필드를 중심으로 구조화되어야 합니다.

`media.mediaTimed` 필드를 사용하는 다른 모든 흐름은 영향을 받으며 논리 업데이트가 필요합니다.

## 다음 단계 및 지원

스트리밍 미디어용 Adobe Data Collection을 사용하는 모든 고객은 지정된 전환 기간 내에 마이그레이션을 완료해야 합니다.

문의 사항이나 지원 요구 사항이 있으면 언제든지 Adobe 지원 팀에 문의하십시오.
