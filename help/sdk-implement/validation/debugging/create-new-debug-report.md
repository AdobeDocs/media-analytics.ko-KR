---
title: 새 디버그 보고서 만들기
description: 이 항목에서는 새 디버그 보고서를 만드는 방법에 대해 설명합니다.
uuid: 438fde3d-98f9-46d1-9672-75d204361568
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 새 디버그 보고서 만들기{#create-a-new-debug-report}

새 디버그 보고서를 만들려면 다음을 수행하십시오.

1. In [!UICONTROL Create New Debug Report] select the following:

   ![](assets/create-new-debug-report.png)

1. 다음 정보를 사용하여 필드를 작성합니다.

   * **보고서 이름을 지정합니다.** - 인증 중에 플레이어를 쉽게 추적하고 브랜드 및 플랫폼을 독립적으로 유지할 수 있도록 플레이어 이름 및 날짜를 입력합니다.
   * **Adobe Analytics**

      * [!UICONTROL 사용자 이름] 및 [!UICONTROL 공유 비밀] - 이러한 필드는 선택 사항이지만, 보고서 세트에 대한 변수 이름 및 변수 설정을 표시하기 위해 웹 서비스 API 자격 증명을 Adobe Debug에 추가할 수 있습니다.

         다음 중 한 방법으로 액세스할 수 있습니다.

         * [!UICONTROL Analytics &gt; 관리 &gt; 회사 설정 &gt; 웹 서비스]
         * [!UICONTROL Analytics &gt; 관리 &gt; 사용자 관리 &gt; 사용자 &gt; 개별 사용자 설정] 새 사용자에 대한 웹 서비스 API 자격 증명을 작성하려면 [!UICONTROL 사용자 관리]에서 사용자를 **웹 서비스 액세스** 사용자 그룹에 추가합니다.
      * [!UICONTROL 기본 끝점] - 이 필드의 데이터는 Adobe에서 제공하며 변경할 수 없습니다.
      * [!UICONTROL 추가 끝점] - `CNAMES`사용하는 경우 추적 서버에 `metrics.companyname.com`
   * **비디오 하트비트(미디어 분석)**

      * [!UICONTROL 기본 끝점] - 이 필드의 데이터는 Adobe에서 제공하며 변경할 수 없습니다.
      * [!UICONTROL 추가 끝점] - `CNAMES``metrics.companyname.com`사용하는 경우 추적 서버(예:



