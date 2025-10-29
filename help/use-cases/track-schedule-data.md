---
title: 예약 데이터를 업로드하여 라이브 콘텐츠 추적
description: 라이브 콘텐츠를 추적하기 위해 일정 데이터를 업로드하는 방법을 알아봅니다.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: 875c4513-ea4e-4c5f-bfc1-34ea175007ca
source-git-commit: 65cd7987acb677b4f4c863b42dc809b5a23c2ed1
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 5%

---

# 예약 데이터를 업로드하여 라이브 콘텐츠 추적

>[!AVAILABILITY]
>
>이 문서에서 설명하는 기능은 릴리스의 제한된 테스트 단계에 있으며 사용자 환경에서 아직 사용하지 못할 수 있습니다. 기능이 일반적으로 제공되면 이 메모는 제거됩니다. 릴리스 프로세스에 대한 정보는 [Customer Journey Analytics 기능 릴리스](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/releases/releases)를 참조하십시오.

이전 라이브 스트리밍 미디어 콘텐츠의 예약 데이터를 업로드하여 라이브 콘텐츠의 시청률을 보다 쉽고 정확하게 추적할 수 있습니다. 개별 프로그램 및 특정 주제나 프로그램 세그먼트에 대한 시청률을 추적할 수 있습니다.

다음은 일정 데이터 업로드가 지원되는 라이브 콘텐츠의 예입니다.

* FAST(무료 광고 지원 TV) 플랫폼

* 로컬 스트림

* 라이브 스포츠

* 뉴스 또는 주제 프로그래밍

## 기능

이전 라이브 스트리밍 미디어 콘텐츠의 데이터 업로드 예약 을 사용할 때 다양한 기능을 사용할 수 있습니다. 이 섹션에서는 프로그램 성능을 분석하는 데 도움이 되는 몇 가지 주요 기능에 대해 설명합니다.

이러한 기능은 스트리밍 미디어 컬렉션을 어떻게 구현하든 관계없이 사용할 수 있습니다.

* **프로그램 일정을 정확하게 추적**: 분석하려는 기간 동안 라이브 스트림에 있는 각 개별 프로그램의 시작 및 종료 시간을 식별합니다. 정확한 시작 및 종료 시간으로 정확한 실행 시간이 정확하게 반영되며 각 뷰어 세션에 대해 분석할 수 있습니다.

  예를 들어, 정확한 시작 및 종료 시간이 항상 라이브 스포츠 이벤트로 알려지지는 않는 한 이벤트가 종료됩니다. 데이터 업로드 일정을 예약하면 프로그램 완료 후 시작 및 종료 시간을 업데이트하여 정확한 보고를 받을 수 있습니다.

* **개별 주제 또는 프로그램 세그먼트 추적**: 특정 프로그램 내의 특정 주제 또는 프로그램 세그먼트(시간 슬롯)에 대한 시간 기반 차원을 새로 만듭니다. 이러한 시간 기반 차원을 사용하면 프로그램의 시청률을 보다 특정 수준으로 분석할 수 있으므로 가장 공감하는 주제나 프로그램 세그먼트에 대한 인사이트를 수집할 수 있습니다.

  예를 들어 축구 경기와 같은 라이브 스포츠 이벤트를 분석할 때 전반부, 반반부 및 후반부에 대해 별도의 차원을 만들 수 있습니다. 이러한 방식으로 프로그램 내의 특정 주제 또는 세그먼트를 추적하면 뷰어 동작을 보다 자세히 분류할 수 있습니다.

* **Journey Optimizer에서 사용자 여정 작성**: 특정 세션에서 열람한 프로그램(또는 열람한 항목이나 프로그램 세그먼트)을 추적한 다음 Adobe Journey Optimizer에서 이 데이터를 사용하여 특정 프로그램을 시청한 고객 또는 특정 주제에 관심을 보인 고객을 위한 사용자 여정을 작성합니다.

## 스트리밍 미디어에 대해 예약 데이터가 작동하는 방식 이해

스트리밍 미디어에 대한 데이터 예약 기능은 다음과 같은 방식으로 작동합니다.

1. 예약 프로그램 레코드에 대한 예약 프로그램 데이터 세트에서 읽으며, 예약 날짜별로 필터링합니다.

   과거에 24시간에서 48시간 발생한 프로그램에서만 작동한다.

2. 예약 프로그램 레코드의 날짜 및 XDM 경로별로 필터링하여 미디어 데이터 집합에서 미디어 닫기 이벤트를 읽습니다.

3. 각 미디어 닫기 이벤트에 대해 미디어 세션과 겹치는 표시가 있으므로 동일한 수의 미디어 예약 시작 이벤트가 생성됩니다.

   각 미디어 예약 시작 이벤트에는 예약의 이름과 길이가 포함됩니다.

   또한 **scheduleTimePlayed**&#x200B;이라는 새 시간 지표에는 미디어 세션이 예약된 프로그램과 겹치는 시간(초)이 포함됩니다. 예약 시작 이벤트의 타임스탬프는 표시가 시작된 시점의 타임스탬프입니다.

4. AEP 미디어 데이터 세트에 새 예약 시작 이벤트를 기록합니다.

## 사전 요구 사항

이전 라이브 콘텐츠의 예약 데이터를 업로드하려면 Streaming Media 환경이 다음 사전 요구 사항을 충족해야 합니다.

* [추적 개요](/help/use-cases/track-av-playback/track-core-overview.md)에 설명된 대로 예약 데이터를 업로드할 콘텐츠를 추적할 수 있도록 스트리밍 미디어 컬렉션을 활성화해야 합니다. <!--specifics??? -->

* Customer Journey Analytics에서 스트리밍 미디어 컬렉션 을 사용합니다. Adobe Analytics에서는 일정 데이터를 업로드하는 기능을 사용할 수 없습니다.

## AEP에서 프로그램 일정 데이터 세트 만들기

예약 정보를 푸시하려면 먼저 Experience Platform에서 프로그램 예약 데이터 세트를 만들어야 합니다.

1. **Media Analytics 예약 프로그램** XDM 클래스를 기반으로 스키마를 만듭니다.

   ![Media Analytics 예약 프로그램 스키마](assets/media_schedule_finish_schema_creation.png)

   Media Analytics 예약 프로그램 클래스의 XDM 정의입니다.

   [https://github.com/adobe/xdm/blob/master/components/fieldgroups/tv-schedule/media-analytics-scheduled-program.schema.json](https://github.com/adobe/xdm/blob/master/components/fieldgroups/tv-schedule/media-analytics-scheduled-program.schema.json)

1. 만든 스키마를 기반으로 데이터 세트를 만듭니다.

1. 다음 섹션 [일정 정보 푸시](#push-schedule-information)을(를) 사용하여 계속합니다.

## 푸시 예약 정보

[프로그램 일정 데이터 세트를 만들기](#create-a-program-schedule-dataset-in-aep)한 후 일정 정보를 푸시할 수 있습니다.

1. 예약 정보를 사용하여 .json 파일을 만듭니다.

   .json 파일에는 XDM 스키마에 따른 예약 프로그램 개체 배열이 포함되어야 합니다.

1. .json 파일 업로드:

   >[!NOTE]
   >
   >이 섹션의 cURL 예제는 다음 변수를 사용합니다.
   >
   >* Adobe Developer을 사용한 인증의 경우:
   >     * 고객 API_키
   >     * AUTH_TOKEN
   >* 조직 id: CUSTOMER_ORG_ID
   >* 설정에서 생성된 레코드 데이터 세트의 데이터 세트 id: DATASET_ID
   >* 파일 업로드에 사용된 첫 번째 요청에서 생성된 배치 id: BATCH_ID
   >* 레코드를 푸시하는 데 사용되는 파일 이름: FILE_NAME

   1. 새 배치를 만든 다음 응답에서 배치 ID를 가져옵니다.

      cURL을 사용하여 새 AEP 배치를 만드는 다음 예를 생각해 보십시오.

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches' \
          -X POST \
          -H 'Accept: application/json' \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>' \
          --data-raw '{"datasetId":"<DATASET_ID>","inputFormat":{"format":"json","isMultiLineJson":true},"tags":{"test":["2"]}}'
      
          HTTP/1.1 201 Created
          {
              "id": "BATCH_ID",
              "imsOrg": "CUSTOMER_ORG_ID",
              "updated": 1749838941763,
              "status": "loading",
              "created": 1749838941763,
              "relatedObjects": [
                  {
                      "type": "dataSet",
                      "id": "DATASET_ID"
                  }
              ],
              "version": "1.0.0",
              ............
          }
      ```

   1. 배치 ID를 사용하여 프로그램 예약 데이터 레코드가 포함된 .json 파일을 푸시합니다.

      일정 정보를 푸시하려면 [일괄 처리 수집 API 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/ingestion/batch/overview)에 설명된 대로 AEP 일괄 처리 API를 사용해야 합니다.

      cURL을 사용하여 일정 레코드가 있는 파일을 푸시하는 다음 예를 생각해 보십시오.

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches/<BATCH_ID>/datasets/<DATASET_ID>/files/<FILE_NAME>' \
          -X PUT \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>' \
          --upload-file ./schedule_21_05_2025.json`
      ```

   1. 배치를 완료합니다.

      cURL을 사용하여 배치를 완료하는 다음 예를 생각해 보십시오.

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches/<BATCH_ID>?action=COMPLETE' \
          -X POST \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>'
      ```

1. 다음 섹션을 계속합니다. [Adobe 고객 지원 센터에 지원 티켓을 기록](#log-a-support-ticket-with-adobe-customer-care).

## Adobe 고객 지원 센터에 지원 티켓 기록

다음 정보를 사용하여 Adobe 고객 지원 센터에 지원 티켓을 기록합니다.

* **미디어 데이터 세트**: 미디어 세션 데이터를 읽을 데이터 세트의 데이터 세트 ID를 지정합니다.

* **일정 데이터 세트**: 일정 레코드를 푸시할 데이터 세트의 데이터 세트 ID를 지정합니다.

* **출력 미디어 데이터 세트**: 일정 시작 이벤트가 저장되는 데이터 세트의 데이터 세트 ID를 지정합니다.

  이 데이터 세트 ID는 미디어 데이터 세트에 사용되는 것과 동일한 데이터 세트 ID일 수 있습니다. 다른 데이터 세트 ID인 경우 미디어 데이터 세트와 동일한 XDM 스키마를 가져야 합니다.

* **조직 ID**: 조직 ID를 지정하십시오.

## 두 개의 레코드가 있는 스케줄 .json 파일의 예

다음 예제는 두 개의 레코드가 있는 .json 예약 파일입니다. 각 .json 파일에는 하루 동안 예약된 모든 프로그램이 포함되어야 합니다.

```
   [
        {
            "_id": "any_identifier_as_id_1",
            "customMetadata": [
                {
                    "name": "Sample value",
                    "value": "Sample value"
                }
            ],
            "defaultMetadata": {
                "album": "Sample value",
                "artist": "Sample value",
                "assetID": "Sample value",
                "author": "Sample value",
                "cdn": "Sample value",
                "dayPart": "Sample value",
                "episode": "Sample value",
                "feed": "Sample value",
                "firstAirDate": "Sample value",
                "firstDigitalDate": "Sample value",
                "genreList": [
                    "Sample value"
                ],
                "label": "Sample value",
                "network": "Sample value",
                "originator": "Sample value",
                "publisher": "Sample value",
                "rating": "Sample value",
                "season": "Sample value",
                "show": "Sample value",
                "showType": "Sample value",
                "station": "Sample value",
                "streamFormat": "Sample value"
            },
            "mediaProgramDetails": {
                "length": 1800,
                "name": "Show Name",
                "startTimestamp": "2025-05-01T00:30:00+00:00"
            },
            "scheduleDate": "2025-05-01",
            "scheduleFilter": {
                "filterPath": "xdm.mediaReporting.sessionDetails.channel",
                "filterValue": "Channel Name"
            },
        },
        {
            "_id": "any_identifier_as_id_2",
            "customMetadata": [
                {
                    "name": "Sample value",
                    "value": "Sample value"
                }
            ],
            "defaultMetadata": {
                "album": "Sample value",
                "artist": "Sample value",
                "assetID": "Sample value",
                "author": "Sample value",
                "cdn": "Sample value",
                "dayPart": "Sample value",
                "episode": "Sample value",
                "feed": "Sample value",
                "firstAirDate": "Sample value",
                "firstDigitalDate": "Sample value",
                "genreList": [
                    "Sample value"
                ],
                "label": "Sample value",
                "network": "Sample value",
                "originator": "Sample value",
                "publisher": "Sample value",
                "rating": "Sample value",
                "season": "Sample value",
                "show": "Sample value",
                "showType": "Sample value",
                "station": "Sample value",
                "streamFormat": "Sample value"
            },
            "mediaProgramDetails": {
                "length": 3600,
                "name": "Show Name 2",
                "startTimestamp": "2025-05-01T01:00:00+00:00"
            },
            "scheduleDate": "2025-05-01",
            "scheduleFilter": {
                "filterPath": "xdm.mediaReporting.sessionDetails.channel",
                "filterValue": "Channel Name"
            }
        }
    ]
```

### 이 예제의 예약 프로그램 필드 이해

1. **mediaProgramDetails**: 일정 시작 이벤트를 만드는 데 필요한 최소 정보를 포함해야 합니다.
   * **startTimestamp**: 표시가 시작된 시간입니다.
   * **이름**: 친숙한 쇼의 이름입니다.
   * **length**: 표시가 지속된 시간(초)입니다.

     >[!IMPORTANT]
     >
     >예약 데이터 요청이 여러 개 있는 경우 시작 및 종료 시간이 겹칠 수 없습니다.

1. **scheduleDate**: 프로그램이 방송된 날짜입니다. 형식은 YYYY-MM-DD여야 합니다. 일정 데이터 세트를 필터링하고 adobe에서 일정을 만드는 모든 일정이 시작되도록 하는 데 사용됩니다.
1. **scheduleFilter**: 모든 미디어 세션 닫기 이벤트를 필터링하는 데 사용됩니다.
   * **filterPath**: 필터링에 사용되는 필드의 XDM 경로입니다.
   * **filterValue**: 필터링에 사용되는 값입니다.
1. **customMetadata**: 일정에 추가하려는 사용자 지정 메타데이터가 이벤트를 시작합니다. 이 메타데이터는 세션 닫기 이벤트에 있는 사용자 지정 메타데이터를 덮어쓰는 데 사용됩니다.
1. **defaultMetadata**: 미디어 닫기 호출에 있는 기본 메타데이터를 추가하거나 덮어쓸 수 있는 특정 차원 목록입니다.

   만든 다음 Customer Journey Analytics에서 보고할 수 있는 차원의 다음 예를 고려하십시오.

   * **[&quot;_에피소드 이름_&quot;](https://experienceleague.adobe.com/ko/docs/media-analytics/using/implementation/variables/audio-video-parameters#episode)**: 이 차원은 특정 시리즈의 가장 성과가 좋은 에피소드를 학습하는 데 도움이 될 수 있습니다.

   * **[자산 ID](https://experienceleague.adobe.com/ko/docs/media-analytics/using/implementation/variables/audio-video-parameters#asset-id)**

1. [Customer Journey Analytics에서 데이터 분석](#analyze-data-in-customer-journey-analytics)을 계속합니다.

## Customer Journey Analytics에서 데이터 분석

[일정 데이터 파일 요청 및 업로드](#request-and-upload-the-schedule-data-file)에 설명된 대로 데이터 파일을 업로드한 후 하루 안에 데이터가 Customer Journey Analytics에서 보고할 준비가 되었습니다.

Customer Journey Analytics에서 과거 Live Streaming Media 데이터에 대해 보고하려면 다음을 수행하십시오.

1. 새 프로젝트를 만들거나 기존 프로젝트를 엽니다.

1. 과거의 라이브 스트리밍 미디어 데이터를 분석하는 데 필요한 테이블 또는 시각화를 만들어 프로젝트를 빌드합니다.

   프로젝트를 작성할 때 예약 데이터 파일에 포함하여 Adobe 고객 지원 센터에 전송한 정보를 사용합니다. 여기에는 일치하는 키, 차원 및 추가 메타데이터가 포함됩니다. 자세한 내용은 [일정 데이터 파일 요청 및 업로드](#request-and-upload-the-schedule-data-file)를 참조하십시오.




<!-- 

Extra

Things they need to upload:
Everything on that slide + other metadata
You can't overlap 2 schedules.
You can build a journey in AJO for the people who watch Mike, Mike, and Mike. e.g. 
This is recurring.
Available to all SKUs? "Increases cost for updated data by 22%, but included in the new higher tier Streaming Media SKU."

You can now upload schedule data of past live content to more easily and accurately track viewership. Live content includes content from FAST (Free Ad Supported TV) platforms or local streams.
You can track which programs a person viewed in a given session, or even which topics or program segments they viewed. These capabilities are available regardless of how you implemented Streaming Media Collection.
Previously, it was difficult to accurately tie a given session to specific programs when analyzing live content, and it wasn't possible to tie a given session to individual topics or program segments.
Schedule data uploads of live content in Streaming Media Collection includes the following capabilities:
Upload schedules for past live content, regardless of your Streaming Media Collection implementation.
Identify the start and end times of each individual program in the live stream for the period of time that you want to analyze. With accurate start and end times, the precise running time is accurately reflected and can be analyzed against each viewer session.
For example, precise beginning and end times are not always known for a live sporting event until the event is over. Schedule data uploads allow you to get accurate reporting by updating the start and end times after the program finishes.
Create new time-based dimensions for specific topics or program segments (time slots) within a given program. These time-based dimensions allow you to analyze viewership of a program at a more specific level, helping to gather insights about which topics or program segments resonated best.
For example, when analyzing a live sporting event, such as a soccer match, you can create separate dimensions for the first half, half time, and second half. This allows for more detailed breakdowns of viewer behavior for specific segments of a program.
These capabilities allow you to:
Analyze show viewership to understand performance.
Target users based on program viewership.
Analyze viewership based on metadata like topic, sports league, sponsorship, and so forth.
Target based on metadata viewership.
Correct media metrics for show dimensions of live sports/events for easier analysis at scale.
Increased ease of use for live sports

-->
