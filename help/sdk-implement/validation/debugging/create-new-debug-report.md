---
seo-title: 새 디버그 보고서 만들기
title: 새 디버그 보고서 만들기
uuid: 438 FDE 3 D -98 F 9-46 D 1-9672-75 D 204361568
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

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
      * [!UICONTROL extra endpoint] `CNAMES`- `metrics.companyname.com`
   * **비디오 하트비트 (Media Analytics)**

      * [!UICONTROL 기본 끝점] - 이 필드의 데이터는 Adobe에서 제공하며 변경할 수 없습니다.
      * [!UICONTROL extra endpoints] - add `CNAMES`(if you use them, for your tracking server, e. g., `metrics.companyname.com`).



