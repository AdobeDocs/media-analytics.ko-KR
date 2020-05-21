---
title: 미디어 분석 SDK 지원 종료 FAQ
description: 이 항목에는 Media Analytics SDK에 대한 지원 종료에 대한 FAQ가 포함되어 있습니다.
translation-type: tm+mt
source-git-commit: 300eb77858296f0246a2cb484386c0dcdf8b87b9
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 2%

---


# 미디어 분석 SDK 지원 종료 FAQ

2021년 8월 31일에 버전 4 Mobile SDK에 대한 지원이 종료됨에 따라 Adobe는 iOS 및 Android용 Media Analytics SDK에 대한 지원을 종료할 예정입니다. 2021년 8월 31일 이후에는 Adobe는 수정 사항, OS 관련 업데이트 또는 Media Analytics SDK에 대한 지원을 제공하지 않습니다.  이러한 새로운 Experience Platform SDK로 마이그레이션하는 동안에는 오디오 및 비디오용 Adobe Analytics를 활성화하려면 [미디어 분석 익스텐션을](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) 구현해야 한다는 점을 유의하십시오.

## Top 5 Things to Know

1. 모바일 v4 SDK는 2021년 8월 31일 이후로 더 이상 지원되지 않습니다. iOS 및 Android용 Adobe Experience Platform(AEP) SDK로 마이그레이션해야 합니다.

1. 오디오 및 비디오용 분석 구현에는 AEP SDK가 필요하며 분석 및 미디어 분석 익스텐션을 사용해야 합니다. 2021년 9월 1일부터 새로운 AEP SDK 및 익스텐션을 사용해야 합니다.  미디어 분석 익스텐션은 Adobe Launch를 사용하여 구성됩니다.  자세한 내용은 독립 [실행형 미디어 SDK에서 Adobe Launch로 마이그레이션을 참조하십시오.](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. iOS 및 Android용 미디어 분석 SDK에 대한 기능 개발이 종료되었습니다.  2019년 가을부터 도입된 새로운 기능은 미디어 분석 확장 기능 및 미디어 컬렉션 API를 사용하여 활성화됩니다.

1. Roku 및 Chromecast SDK는 오디오 및 비디오 고객을 위한 Analytics에서 계속 사용할 수 있습니다. Roku 및 Chromecast SDK는 독립 실행형 SDK로 지속적으로 향상되고 지원됩니다.  미디어 분석용 JS SDK를 사용하는 경우 독립형 SDK를 계속 사용하거나 Adobe Launch를 사용하여 미디어 분석 익스텐션을 활성화할 수 있습니다.

1. 2021년 9월 1일 이전에 Adobe는 자체적인 재량에 따라 높은 기술적 영향이나 비즈니스 노출 문제에 대한 새로운 수정 사항을 개발할 수 있습니다. Adobe는 고객의 의견에 따라 영향과 노출의 정도와 그에 따른 활동을 결정합니다.

문의 사항이 있는 경우 Adobe 고객 성공 관리자에게 문의하십시오.

## FAQ

1. **Roku 및 Chromecast SDK에 대한 지원은 영향을 &#x200B; 받습니까?**

   아니요.  Roku 및 Chromecast SDK는 당분간 독립 실행형 SDK로 계속 &#x200B; 지원됩니다&#x200B;.
1. **Media Analytics JS SDK 구현이 이러한 변경의 영향을 &#x200B; 받습니까?**

   아니요.  미디어 분석용 JS SDK를 사용하는 고객은 Adobe Launch를 통해 SDK를 계속 사용하거나 활성화할 수 있습니다.
&#x200B;
1. **미디어 분석 익스텐션으로 마이그레이션하기 위한 노력 &#x200B; 수준은 무엇입니까?**

   LOE는 각 고객의 구현에 따라 다르므로 다양한 효과를 얻을 수 있습니다.  아래의 마이그레이션 설명서를 검토한 후 추가 지원을 받으려면 컨설팅 및/또는 고객 지원 센터에 문의하십시오.

   [미디어 분석 확장: Android 마이그레이션](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [미디어 분석 확장: iOS 마이그레이션](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [미디어 분석 확장: 새로운 구현](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **Launch를 태그 관리 시스템으로 사용해야 합니까? Launch를 사용하지 않으려면 어떻게 해야 합니까?**

   모바일의 경우 Mobile Services UI와 같은 미디어 확장을 구성하려면 Launch가 필요합니다. 모바일 앱 사용 사례에서는 태그 관리 시스템으로 사용되지 않습니다.

1. **이러한 지원이 tvOS용 SDK에 영향을 미칩니까?**

   예. tvOS(버전 10+)의 경우 권장되는 구현은 미디어 분석 익스텐션으로 마이그레이션하는 것입니다.  AEP SDK 지원 및 Media Analytics Extension 지원은 2020년 6월에 제공될 예정입니다.  자세한 내용은 독립형 Media SDK에서 [Adobe Launch - iOS로 마이그레이션을 참조하십시오](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html).

1. **이러한 지원이 FireTV 및 AndroidTV용 SDK에 영향을 미칩니까&#x200B;?**

   예. FireTV 및 AndroidTV의 경우 권장되는 구현은 미디어 분석 익스텐션으로 마이그레이션하는 것입니다.  AEP SDK 지원 및 Media Analytics Extension 지원은 2020년 6월에 제공될 예정입니다.  자세한 내용은 독립형 Media SDK에서 [Adobe Launch - Android로 마이그레이션을 참조하십시오](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html).
