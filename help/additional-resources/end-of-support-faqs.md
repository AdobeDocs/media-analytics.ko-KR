---
title: 자세한 내용은 Media Analytics SDK 지원 종료 FAQ에 대해 알아봅니다.
description: 이 항목에는 Media Analytics SDK에 대한 지원 종료 FAQ가 포함되어 있습니다.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '690'
ht-degree: 100%

---

# Media Analytics Mobile SDK 지원 종료 FAQ

2021년 8월 31일에 버전 4 Mobile SDK에 대한 지원이 종료됨에 따라 Adobe는 iOS 및 Android용 Media Analytics Mobile SDK에 대한 지원도 종료할 예정입니다. 2021년 8월 31일 이후 Adobe는 수정 사항, OS 관련 업데이트 또는 Media Analytics Mobile SDK에 대한 지원을 제공하지 않습니다.  새로운 Experience Platform SDK로 마이그레이션하는 동안 스트리밍 미디어용 Adobe Analytics를 활성화하려면 [Media Analytics 확장](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)을 구현해야 한다는 점을 유의하십시오.

>[!NOTE]
>Adobe Experience Platform Launch는 Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=ko-KR)를 참조하십시오.


## 알아 두어야 할 상위 5가지 항목

1. 모바일 v4 SDK는 2021년 8월 31일 이후로 더 이상 지원되지 않습니다. iOS 및 Android용 Adobe Experience Platform(AEP) 모바일 SDK로 마이그레이션해야 합니다. 자세한 내용은 [버전 4 Mobile SDK의 지원 종료 FAQ](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq)를 참조하십시오.

1. 스트리밍 미디어용 분석 구현에는 AEP Mobile SDK가 필요하고 Analytics 및 Media Analytics 확장을 사용해야 합니다. 2021년 9월 1일부터 새로운 AEP Mobile SDK 및 확장을 사용해야 합니다.  Media Analytics 확장 기능은 Adobe 태그를 사용하여 구성됩니다(데이터 수집).  자세한 내용은 [독립 실행형 Media SDK에서 Adobe Launch로 마이그레이션](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md)을 참조하십시오.

1. iOS 및 Android용 Media Analytics SDK에 대한 기능 개발이 종료되었습니다.  2019년 가을부터 도입된 새로운 기능은 Media Analytics 확장 기능 및 Media Collection API를 사용하여 활성화됩니다.

1. 스트리밍 미디어용 Analytics 고객은 Roku 및 Chromecast SDK를 계속 사용할 수 있습니다. Roku 및 Chromecast SDK는 독립 실행형 SDK로 지속적으로 향상되고 지원됩니다.  Media Analytics용 JS SDK를 사용하는 경우 독립형 SDK를 계속 사용하거나 Adobe 데이터 수집(전, Adobe Launch)를 사용하여 Media Analytics 확장 기능을 활성화할 수 있습니다).

1. 2021년 9월 1일 이전에 Adobe는 재량에 따라 높은 기술적 영향이나 비즈니스 노출 문제에 대한 새로운 수정 사항을 개발할 수 있습니다. Adobe는 고객의 의견에 따라 영향과 노출의 정도와 그에 따른 활동을 결정합니다.

질문이 있는 경우 Adobe 고객 성공 관리자에게 문의하십시오.

## FAQ

1. **Roku 및 Chromecast SDK에 대한 지원은 영향을 받습니까?**

   아니요.  Roku 및 Chromecast SDK는 당분간 독립 실행형 SDK로 계속 지원됩니다.&#x200B;
&#x200B;
1. **Media Analytics JS SDK 구현이 이 변경의 영향을 받습니까?**

   아니요.  Media Analytics용 JS SDK를 사용하는 고객은 Adobe Launch를 통해 SDK를 계속 사용하거나 활성화할 수 있습니다.
&#x200B;
1. **Media Analytics 확장 기능으로 마이그레이션하기 위한 작업 수준은 무엇입니까?**

   LOE는 각 고객의 구현에 따라 다르므로 다양한 효과를 얻을 수 있습니다.  아래의 마이그레이션 설명서를 검토한 후 추가 지원을 받으려면 컨설팅 및/또는 고객 지원 센터에 문의하십시오.

[Media Analytics 확장 기능: Android 마이그레이션](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

[Media Analytics 확장 기능: iOS 마이그레이션](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [Media Analytics 확장 기능: 새로운 구현](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **Launch를 태그 관리 시스템으로 사용해야 합니까? Launch를 사용하지 않으려면 어떻게 해야 합니까?**

   모바일 앱 사용 사례의 경우, Launch는 웹용 태그 관리 시스템으로 사용되지 않습니다.  SDK 확장자를 구성하려면 Launch UI가 필요합니다. 이는 Adobe Mobile Services UI를 사용하여 모바일 v4 SDK를 구성하는 방법과 유사합니다. 설치 시 Launch를 사용하면 사용자가 선택한 확장자에 따라 사용자 정의된 설치 지침이 제공된다는 이점이 있습니다.

1. **이러한 지원이 tvOS용 SDK에 영향을 미칩니까?**

   예. tvOS(버전 10+)의 경우 권장되는 구현은 Media Analytics 확장 기능으로 마이그레이션하는 것입니다.  자세한 내용은 [독립 실행형 Media SDK에서 Adobe Launch - iOS로 마이그레이션](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)을 참조하십시오.

1. **이러한 지원이 Fire TV 및 AndroidTV용 SDK에 영향을 미칩니까?**

   예. Fire TV 및 AndroidTV의 경우 권장되는 구현은 Media Analytics 확장 기능으로 마이그레이션하는 것입니다.  자세한 내용은 [독립 실행형 Media SDK에서 Adobe Launch - Android로 마이그레이션](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)을 참조하십시오.