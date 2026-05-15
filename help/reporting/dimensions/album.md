---
title: 앨범
description: 오디오 트랙이 속한 앨범을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 10%

---


# 앨범

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**앨범**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [앨범](/help/implementation/variables/standard-metadata/album.md)을 참조하세요.*

>[!ENDSHADEBOX]

**앨범** 차원은 오디오 트랙이 속한 앨범을 보고합니다(예: `"Pinegrove"`). 이 링크를 사용하여 동일한 앨범의 트랙에 걸쳐 참여를 롤업할 수 있습니다.

## 이 차원이 채워지는 방법

앨범은 오디오 콘텐츠에 대한 세션 시작 시 플레이어가 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 오디오 메타데이터]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.album`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.album`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videoaudioalbum` |
| Audience Manager | `c_contextdata.a.media.album` |

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 앨범 제목입니다. 각기 다른 아티스트의 같은 제목을 가진 두 앨범이 하나의 라인 아이템으로 무너진다. [아티스트](artist.md) 차원과 연결하여 명확성을 유지하십시오.
