---
title: Adobe 스트리밍 미디어 서비스를 위한 사전 요구 사항에 대해 알아봅니다.
description: 스트리밍 미디어 서비스를 시작합니다. 구현에 필요한 사항을 알아봅니다.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/e9iYwDwT-zSSZ3hV20U1w7p-MtKaK4Q8-vGMCrnenpc
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: b18eab3deb3d15a08adf2f7ecf61d73235bbc6e5
workflow-type: tm+mt
source-wordcount: 274
ht-degree: 10%

---

# 사전 요구 사항 {#prerequisites}

Adobe 스트리밍 미디어 서비스 구현을 시작하기 전에 다음 작업을 완료하십시오.

1. **가격 책정 모델 확인**<br>
Customer Journey Analytics 스트리밍 미디어 컬렉션 추가 기능 및 스트리밍 미디어용 Adobe Analytics 추가 기능의 현재 가격 모델은 비디오 스트림을 기반으로 합니다. 추가 기능은 Adobe Analytics 및 Adobe용으로 별도로 판매되므로 필요한 경우 영업 담당자 또는 Adobe Experience Platform 계정 팀에 문의하십시오.

1. **Adobe Analytics 보고서 활성화** *(Analytics 전용 구현)*<br>
Analytics에서 보고서를 활성화하고 수집 중인 콘텐츠 및 광고 데이터를 보려면 보고서를 활성화해야 합니다. [Analytics 전용 구현에 대한 보고 설정](/help/reporting/setup/analytics-reporting.md)을 참조하십시오.

1. **ID 구성**<br>

   ID 구성 요구 사항은 구현 방법에 따라 다릅니다.

   * **Edge 구현**: ID는 Adobe Experience Platform ID 네임스페이스 구성을 통해 처리됩니다. 별도의 ID 서비스 설정이 필요하지 않습니다. 자세한 내용은 [Edge 구현 개요](/help/implementation/edge/overview.md)를 참조하십시오.

   * **Analytics 전용 구현**: CX 엔터프라이즈 솔루션에서 방문자를 일관되게 식별하려면 Adobe Experience Platform ID 서비스를 사용하도록 설정해야 합니다. ID 서비스는 각 사이트 방문자에게 고유한 영구 ID를 할당하여 구독하는 모든 CX 엔터프라이즈 솔루션에서 해당 ID를 공유할 수 있도록 합니다.

     자세한 내용은 [Adobe Experience Platform Identity Service 설명서](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ko)를 참조하세요.

1. **구현 방식에 대한 추가 사전 요구 사항 보기**

   스트리밍 미디어 서비스를 구현하는 방법에 따라 다음 구현 방법 중 하나에 대한 사전 요구 사항을 확인하십시오.

   * [Analytics 전용 구현 개요](/help/implementation/analytics-only/overview.md)

   * [Edge 구현 개요](/help/implementation/edge/overview.md)

   본인에게 적합한 구현 방식을 찾아보려면 [구현 개요](/help/implementation/overview.md)를 참조하십시오.
