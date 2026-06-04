---
title: 스트리밍 미디어용 새 Adobe Analytics 데이터 유형으로 대상자 마이그레이션
description: 스트리밍 미디어용 새로운 Adobe Analytics 데이터 유형으로 대상자를 마이그레이션하는 방법을 알아봅니다
feature: Streaming Media
role: User, Admin, Developer
exl-id: 67e67a4b-bd61-4247-93b7-261bd348d29b
TQID: https://experienceleague.adobe.com/Y-Y-xWKm-zOzaQm8kMbgGx8r6BTNLl-Q5AltlF5v7aA
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 92e1a77339d29b0ef7ec8adc76817b2ac61ee900
workflow-type: tm+mt
source-wordcount: 759
ht-degree: 1%

---

# 새 스트리밍 미디어 필드를 사용하도록 Customer Journey Analytics 마이그레이션

이 문서에서는 &quot;Media&quot;라는 Adobe 스트리밍 미디어 서비스 데이터 유형을 사용하는 Customer Journey Analytics 설치를 업데이트하여 &quot;[미디어 보고 세부 정보](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;이라는 새로운 해당 데이터 유형을 사용해야 하는 방법에 대해 설명합니다.

## Customer Journey Analytics 마이그레이션

Customer Journey Analytics 설정을 이전 데이터 형식인 &quot;Media&quot;에서 새 데이터 형식인 &quot;[미디어 보고 세부 정보](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;(으)로 마이그레이션하려면 이전 데이터 형식을 사용하는 다음 설정을 업데이트해야 합니다.

* 데이터 보기

* 파생 필드

### 데이터 보기 마이그레이션

데이터 보기를 새 데이터 유형으로 마이그레이션하려면 다음을 수행합니다.

1. 더 이상 사용되지 않는 &quot;미디어&quot; 데이터 유형을 사용하여 모든 데이터 보기를 찾습니다. 경로가 `media.mediaTimed`(으)로 시작되는 모든 필드입니다.

1. 다음 중 하나를 수행합니다.

   * 이러한 데이터 보기에서 새 &quot;미디어 보고 세부 정보&quot; 데이터 유형의 필드를 삽입합니다.

   * 설정된 경우 새 &quot;미디어 보고 세부 정보&quot; 데이터 유형을 사용하고, &quot;미디어 보고 세부 정보&quot; 데이터 유형이 설정되지 않은 경우 이전 &quot;미디어&quot; 데이터 유형으로 축소되는 파생 필드를 만듭니다.

### 파생 필드 마이그레이션

파생 필드를 새 데이터 유형으로 마이그레이션하려면:

1. 더 이상 사용되지 않는 &quot;미디어&quot; 데이터 유형을 사용하여 파생된 모든 필드를 찾습니다. 경로가 `media.mediaTimed`(으)로 시작하는 필드를 포함하는 모든 파생 필드입니다.

1. 파생된 필드의 모든 이전 필드를 &quot;미디어 보고 세부 정보&quot;의 새 해당 필드로 바꿉니다.

이전 필드와 새 필드 간에 매핑하려면 [콘텐츠 ID](/help/reporting/dimensions/content.md) 매개 변수와 [스트리밍 미디어 서비스](/help/media-overview.md)에 설명된 스트리밍 미디어 변수의 나머지 부분을 참조하십시오. 이전 필드 경로는 &quot;XDM 필드 패스&quot; 속성에서 찾을 수 있고 새 필드 경로는 &quot;보고 XDM 필드 패스&quot; 속성에서 찾을 수 있습니다.

![이전 및 새 XDM 필드 패스](../../assets/field-paths-updated.jpeg)

## 예

마이그레이션 지침을 더 쉽게 따르려면, 더 이상 사용되지 않는 이전 &quot;미디어&quot; 데이터 유형의 필드가 있는 데이터 보기를 포함하는 다음 예를 고려하십시오. 이 데이터 보기에서 새 해당 필드를 추가해야 합니다.

### 데이터 보기 업데이트

다음 옵션 중 하나를 사용하여 데이터 보기를 업데이트할 수 있습니다.

#### 옵션 1

1. 더 이상 사용되지 않는 데이터 유형에서 이전 필드를 사용하는 지표 또는 차원을 찾습니다.

   데이터 보기의 ![이전 필드 경로](../../assets/old-field-data-view.jpeg)

1. [챕터 오프셋](/help/reporting/dimensions/chapter-offset.md) 문서에서 해당 새 필드를 확인하십시오.

1. 데이터 보기에서 새 해당 필드를 찾습니다.

   ![데이터 보기의 새 필드 경로](../../assets/new-field-data-view.jpeg)

1. 새 필드를 지표 또는 차원으로 드래그합니다.

1. 더 이상 사용되지 않는 &quot;미디어&quot; 데이터 유형의 필드를 사용하는 모든 지표 및 차원에 대해 이 프로세스를 반복합니다.

#### 옵션 2

이 옵션은 특정 이벤트에 대한 값이 존재하는 기준으로 이전 필드의 값 또는 새 필드의 값을 선택하는 파생 필드를 만듭니다. 이 파생된 필드는 사용 중인 모든 프로젝트의 이전 &quot;미디어&quot; 데이터 유형을 대체합니다.

설정된 경우 새 &quot;미디어 보고 세부 정보&quot; 데이터 유형을 사용하거나, &quot;미디어 보고 세부 정보&quot; 데이터 유형이 설정되지 않은 경우 이전 &quot;미디어&quot; 데이터 유형으로 대체되는 &quot;챕터 이름&quot;에 대해 파생된 필드를 만들려면:

1. &quot;Case When&quot; 절을 파생된 필드로 드래그합니다.

   ![데이터 보기를 만들려면 새 필드를 사용자 지정](../../assets/create-derived-field2.jpeg)

1. [챕터 이름](/help/reporting/dimensions/chapter-name.md) 페이지에 표시된 대로 **보고 XDM 필드 경로**&#x200B;의 값을 사용하여 **[!UICONTROL If]** 절을 채웁니다.

   ![챕터 이름](../../assets/chapter-name.jpeg)

   ![챕터 이름](../../assets/chapter-name2.jpeg)

   ![파생 필드 조건](../../assets/derived-field-condition.jpeg)

   ![파생 필드 챕터 이름](../../assets/derived-field-chapter-name.jpeg)

1. 더 이상 사용되지 않는 &quot;미디어&quot; 데이터 유형의 이전 필드를 사용하여 대체 값을 채웁니다.

   ![대체 값](../../assets/fallback-value.jpeg)

   ![대체 값](../../assets/fallback-value2.jpeg)

   파생된 필드에 대한 최종 정의입니다.

   ![파생 필드 완료](../../assets/derived-field-complete.jpeg)

1. 파생된 필드를 업데이트하려면 더 이상 사용되지 않는 이전 필드(`media.mediaTimed`(으)로 시작하는 경로)를 사용하는 파생된 필드를 찾으십시오.

   ![파생 필드](../../assets/old-derived-field.jpeg)

1. 업데이트할 파생 필드 위로 마우스를 가져간 다음 **[!UICONTROL 편집]** 아이콘을 선택합니다.

1. 이전 데이터 형식(`media.mediaTimed`(으)로 시작하는 경로)에서 모든 필드를 찾아 새 해당 필드로 바꿉니다.

   ![이전 데이터 형식의 필드 찾기](../../assets/locate-fields-with-old-datatype.jpeg)

1. [콘텐츠 이름](/help/reporting/dimensions/content-name.md) 문서에서 해당 새 필드를 확인하십시오.

1. 이전 필드를 새 필드로 바꿉니다.

   ![새 필드](../../assets/derived-field-new.jpeg)

1. 더 이상 사용되지 않는 이전 &quot;미디어&quot; 데이터 유형의 필드를 사용하여 파생된 모든 필드에 대해 이 프로세스를 반복합니다.

   CJA 설치 마이그레이션이 완료되었습니다.
