---
title: 사용자 지정 메타데이터 지원 - XDM 형식
description: Experience Edge XDM 형식을 사용하여 미디어 추적 이벤트와 함께 사용자 지정 메타데이터를 보내는 방법에 대해 알아봅니다.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: da2fe856a32f9056752b9e2c2e339d43be20372a
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 5%

---


# 사용자 지정 메타데이터 지원 - XDM 형식

Experience Edge API를 사용하면 `sessionStart`, `adStart` 및 `chapterStart` API 이벤트의 표준 XDM 필드와 함께 미디어 사용자 지정 메타데이터를 보낼 수 있습니다. XDM 형식을 통해 전송된 미디어 사용자 지정 메타데이터는 **Adobe Analytics** 및 **Adobe Experience Platform** 모두에 전달할 수 있습니다.

Media Collection API 구현의 경우 [사용자 지정 메타데이터 지원](/help/implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)을 참조하십시오.

## 개요

미디어 사용자 지정 메타데이터는 Experience Edge 요청 내의 두 위치에서 각각 서로 다른 라우팅 동작을 사용하여 보낼 수 있습니다.

| 위치 | Adobe Analytics으로 전송됨 | Adobe Experience Platform으로 전송됨 | 사용 사례 |
|----------|------------------------|-----------------------------------|----------|
| `xdm.mediaCollection.customMetadata` | ✅ 예 | ✅ 예 | 두 시스템에 필요한 비즈니스 데이터 |
| `_data` | ✅ 예 | ❌ 없음 | Analytics 관련 플래그 또는 처리 힌트 |

사용자 지정 메타데이터는 다음 세 가지 이벤트 유형에 적용됩니다.

| 이벤트 | 메타데이터 적용 대상 |
|-------|-------------------|
| `sessionStart` | 기본 컨텐츠(전체 세션) |
| `adStart` | 개별 광고 |
| `chapterStart` | 컨텐츠 챕터 또는 세그먼트 |

## 구조

### `xdm.mediaCollection.customMetadata`(Analytics + AEP)

사용자 지정 메타데이터는 `mediaCollection` 개체 내의 **이름-값 개체의 배열**&#x200B;입니다.

```json
{
  "xdm": {
    "mediaCollection": {
      "customMetadata": [
        {
          "name": "_tenant.fieldName",
          "value": "fieldValue"
        }
      ]
    }
  }
}
```

&lt;InlineAlert variant="warning" slots="text" />

`customMetadata`은(는) `xdm` 루트 수준이 아닌 `mediaCollection` 내의 **배열**&#x200B;이어야 합니다.

**잘못됨:**

```json
{
  "xdm": {
    "eventType": "media.sessionStart",
    "customMetadata": [...]  // ❌ Wrong location
  }
}
```

**수정:**

```json
{
  "xdm": {
    "eventType": "media.sessionStart",
    "mediaCollection": {
      "customMetadata": [...]  // ✅ Inside mediaCollection
    }
  }
}
```

### `_data`(Analytics 전용)

`_data` 개체는 AEP 데이터 세트를 우회하여 Adobe Analytics에만 데이터를 전송하는 특별한 Experience Edge 구성입니다. 사용자 지정 메타데이터는 `__adobe.analytics.contextData` 아래에 있어야 합니다.

**이름-값 개체 배열**&#x200B;을 사용하는 `xdm.mediaCollection.customMetadata`과(와) 달리 `_data` 매핑은 `contextData` 바로 아래에 있는 플랫 **키-값 개체**&#x200B;를 사용합니다.

| 접근 방식 | 구조 | 목적지 |
|----------|-----------|-------------|
| `xdm.mediaCollection.customMetadata` | `{"name": "...", "value": "..."}`개 개체 배열 | Analytics + AEP |
| `_data.__adobe.analytics.contextData` | 플랫 키-값 개체 `{"key": "value"}` | Analytics 전용 |

```json
{
  "xdm": { ... },
  "_data": {
    "__adobe": {
      "analytics": {
        "contextData": {
          "debugMode": "true",
          "internalTestFlag": "QA-Session"
        }
      }
    }
  }
}
```

### 이름 지정 규칙

- 밑줄을 사용하여 테넌트 네임스페이스가 있는 **XDM 형식:** 접두사입니다. 테넌트 사용자 지정 필드 그룹에 `_<tenant>.<struct_name>.<field_name>`과(와) 같은 구조를 만들 수도 있습니다.
- **`_data`형식:** 필드가 `_data.__adobe.analytics.contextData` 아래에 배치됩니다. 필드 이름에는 밑줄 접두사가 필요하지 않습니다(예: `debugFlag`).

## 기본 컨텐츠 사용자 지정 메타데이터

`sessionStart`(으)로 전송되었습니다. 추적 중인 기본 미디어에 적용되며 광고 및 챕터 호출 전체에서 사용할 수 있습니다. 여기에 정의된 모든 사용자 지정 메타데이터는 해당 닫기 호출 시 미디어 백엔드에 의해 자동으로 병합됩니다. 광고 및 챕터에 대해 정의된 특정 사용자 지정 메타데이터와 함께 포함됩니다.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### 요청

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Sample Video",
            "playerName": "HTML5 Player",
            "contentType": "VOD",
            "length": 3600,
            "channel": "Sports"
          },
          "playhead": 0,
          "customMetadata": [
            {
              "name": "_mycompany.contentCategory",
              "value": "Live Sports"
            },
            {
              "name": "_mycompany.leagueType",
              "value": "Professional"
            }
          ]
        },
        "timestamp": "2026-03-10T18:00:00Z"
      }
    }
  ]
}'
```

## 사용자 지정 메타데이터 추가

`adStart`(으)로 전송되었습니다. 각 개별 광고에만 해당됩니다. `sessionStart`의 사용자 지정 메타데이터도 여기에 정의된 광고 관련 사용자 지정 메타데이터와 함께 광고 닫기 호출에서 미디어 백엔드에 의해 자동으로 병합됩니다.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### 요청

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
          "sessionID": "your-session-id",
          "playhead": 30,
          "advertisingDetails": {
            "name": "Summer Sale Ad",
            "playerName": "HTML5 Player",
            "length": 30,
            "podPosition": 1
          },
          "customMetadata": [
            {
              "name": "_mycompany.campaignId",
              "value": "SUMMER2026"
            },
            {
              "name": "_mycompany.targetAudience",
              "value": "18-34"
            },
            {
              "name": "_mycompany.adFormat",
              "value": "skippable"
            }
          ]
        },
        "timestamp": "2026-03-10T18:05:30Z"
      }
    }
  ]
}'
```

## 챕터 사용자 지정 메타데이터

`chapterStart`(으)로 전송되었습니다. 각 콘텐츠 챕터 또는 세그먼트에 대한 것입니다. `sessionStart`의 사용자 지정 메타데이터도 여기에 정의된 챕터별 사용자 지정 메타데이터와 함께 챕터 닫기 호출에서 미디어 백엔드에 의해 자동으로 병합됩니다.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### 요청

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
          "sessionID": "your-session-id",
          "playhead": 600,
          "chapterDetails": {
            "friendlyName": "Introduction",
            "length": 300,
            "index": 1,
            "offset": 600
          },
          "customMetadata": [
            {
              "name": "_mycompany.chapterType",
              "value": "tutorial"
            },
            {
              "name": "_mycompany.difficulty",
              "value": "beginner"
            }
          ]
        },
        "timestamp": "2026-03-10T18:10:00Z"
      }
    }
  ]
}'
```

## `_data` 개체 사용(Analytics 전용 메타데이터)

임시 플래그, 디버깅 변수 또는 Analytics 관련 처리 힌트와 같은 Adobe Analytics 데이터 세트에 **저장하지**&#x200B;해야 하는 Analytics의 메타데이터가 필요한 경우 `_data` 개체를 사용합니다.

&lt;InlineAlert variant="warning" slots="text" />

`_data`을(를) 통해 전송된 데이터는 Adobe Experience Platform에 저장되지 않으며 Real-Time CDP, Journey Orchestration 또는 기타 AEP 서비스에 사용할 수 없습니다.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### 요청

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Sample Video",
            "playerName": "HTML5 Player",
            "contentType": "VOD",
            "length": 3600
          },
          "playhead": 0,
          "customMetadata": [
            {
              "name": "_mycompany.league",
              "value": "Action"
            }
          ]
        },
        "timestamp": "2026-03-10T18:00:00Z"
      },
      "_data": {
        "__adobe": {
          "analytics": {
            "contextData": {
              "debugMode": "true",
              "testFlag": "QA-Session"
            }
          }
        }
      }
    }
  ]
}'
```

이 예에서,
- Analytics와 AEP 모두에 `_mycompany.league`을(를) →.
- `debugMode` 및 `testFlag`(`_data.__adobe.analytics.contextData`에서)→ Analytics로만 전송됩니다.


## 다운스트림 데이터 위치

&lt;InlineAlert variant="info" slots="text" />

`xdm.mediaCollection.customMetadata`은(는) 이벤트를 사용하여 사용자 지정 메타데이터를 보내는 데 사용되는 **인바운드 API 경로**&#x200B;입니다. 처리 후 데이터는 컨텍스트 데이터 변수로 Adobe Analytics에 전달되며 `mediaReporting.customMetadata` 및 최상위 병합된 필드로 Adobe Experience Platform에 저장됩니다.

**Adobe Analytics:**
- 처리 후 사용자 지정 메타데이터는 컨텍스트 데이터 변수로 Adobe Analytics에 전달됩니다. `_tenant` 접두사가 자동으로 제거되므로 처리 규칙은 `_tenant` 이후의 필드 경로만 참조합니다(예: `_mycompany.contentCategory`이(가) `contentCategory`이(가) 됨).
- `_data`을(를) 통해 전송된 데이터도 Adobe Analytics으로 전달되며 처리 규칙을 통해 사용할 수 있습니다.
- 처리 규칙을 사용하여 컨텍스트 데이터 변수를 eVar, prop 또는 기타 Analytics 변수에 매핑합니다. 자세한 내용은 [Adobe Experience Platform Edge Network에 대한 데이터 변수 매핑](https://experienceleague.adobe.com/ko/docs/analytics/implementation/aep-edge/data-var-mapping)을 참조하십시오.

**Adobe Experience Platform:**
- 사용자 지정 메타데이터 필드는 XDM 스키마(예: `_mycompany`)에서 사용자 지정 필드로 정의되어야 하며 병합된 필드로 AEP에 저장하고 쿼리할 수 있습니다

  ![XDM 스키마의 사용자 지정 필드 정의](assets/custom_metadata.png)
- 보고 및 쿼리를 위해 사용자 지정 메타데이터는 `mediaReporting.customMetadata`에서 사용할 수 있으며 최상위 병합된 필드로도 사용할 수 있습니다. 사용 사례에 가장 적합한 것을 사용하십시오.
- 세그먼테이션, Journey Orchestration 및 Real-Time CDP 활성화에 액세스 가능

## 비헤이비어

- 모든 사용자 지정 메타데이터 값은 **문자열**&#x200B;이어야 합니다. 보내기 전에 숫자와 부울을 변환합니다.
- `sessionStart` 메타데이터는 전체 세션 동안 지속되며 업데이트에는 새 세션이 필요합니다.
- 각 `adStart` 및 `chapterStart` 이벤트는 서로 다른 사용자 지정 메타데이터를 전달할 수 있습니다.
- 표준 필드가 있는 경우 사용자 지정 메타데이터보다 표준 XDM 필드(`sessionDetails`, `advertisingDetails`, `chapterDetails`) 우선


## 관련 설명서

- [사용자 지정 메타데이터 지원](/help/implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md). — MC API(JSON 형식)
- [미디어 컬렉션 세부 정보 데이터 형식](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/media-collection-details) — XDM 스키마 참조
- [Adobe Experience Platform Edge Network에 대한 데이터 변수 매핑](https://experienceleague.adobe.com/ko/docs/analytics/implementation/aep-edge/data-var-mapping) - XDM 필드에 대한 Analytics 컨텍스트 데이터 매핑
<!--
- [Session endpoints](sessions.md) — Session lifecycle management
- [Ad endpoints](ads.md) — Track advertising impressions
- [Chapter endpoints](chapters.md) — Segment content into chapters
-->
