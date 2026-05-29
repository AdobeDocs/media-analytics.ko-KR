---
title: 스트림 유형
description: 각 미디어 세션이 오디오 또는 비디오 컨텐츠인지 캡처합니다.
feature: Dimensions
role: User, Admin
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 6%

---


# 스트림 유형

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**스트림 유형**보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [스트림 형식](/help/implementation/variables/core/stream-type.md)을 참조하세요.*

>[!ENDSHADEBOX]

**스트림 유형** 차원은 각 미디어 세션이 오디오 콘텐츠인지 비디오 콘텐츠인지를 캡처합니다. 보고서 세트에 대해 [미디어 코어가 활성화](/help/implementation/media-sdk/setup/media-reports-enable.md)되면 Adobe Analytics에서, 스트리밍 미디어 데이터를 포함하는 데이터 세트에 대해 Customer Journey Analytics에서 사용할 수 있습니다.

## 이 차원이 채워지는 방법

스트림 유형은 세션 시작 시 플레이어에 의해 설정되고 세션 종료 호출로 전달됩니다. 계산 또는 파생되지 않습니다. 보고된 값은 수집 중에 전송된 값과 정확히 일치합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.streamType`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.streamType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videostreamtype` |
| Audience Manager | `c_contextdata.a.media.streamType` |

>[!IMPORTANT]
>
>스트림 유형이 설정되지 않은 경우 해당 세션에 대한 차원이 채워지지 않습니다. 이러한 세션은 내장 오디오 전용 및 비디오 전용 세그먼트에서 제외되며, 스트림 유형 분류와 함께 사용할 경우 모든 스트리밍 미디어 세그먼트는 과소계산됩니다.

## 차원 항목

| 값 | 설명 |
| --- | --- |
| `video` | 세션은 비디오 콘텐츠였습니다. |
| `audio` | 세션은 팟캐스트, 오디오북 또는 음악 스트림과 같은 오디오 콘텐츠였다. |

사용자 지정 값은 컬렉션 API에서 기술적으로 허용되지만 권장되지 않습니다. 이 세그먼트들은 아래에 설명된 기본 제공 세그먼트와 일치하지 않으며, 구현 간에 일관되지 않은 보고를 초래할 수 있습니다.

## 권장 세그먼트

스트림 유형은 Adobe Analytics의 기본 제공 [!UICONTROL 미디어 스트림 유형] 세그먼트의 기초입니다. 이러한 세그먼트를 사용하여 스트리밍 미디어 보고서를 특정 콘텐츠 유형으로 분류할 수 있습니다.

| 세그먼트 | 규칙 |
| --- | --- |
| [!UICONTROL 모든 스트리밍 미디어] | 컨텐츠(ID)가 존재함 |
| [!UICONTROL 오디오만] | 컨텐츠(ID)가 있으며 스트림 유형 = `audio` |
| [!UICONTROL 비디오만] | 콘텐츠(ID)가 있으며 스트림 유형!= `audio`입니다. |

>[!TIP]
>
>[!UICONTROL 비디오 전용] 세그먼트는 스트림 유형이 `audio`이(가) 아닌 사용자 지정 값으로 설정되었을 수 있는 세션을 올바르게 캡처하기 위해 `= video`이(가) 아닌 `!=` 규칙을 사용합니다.
