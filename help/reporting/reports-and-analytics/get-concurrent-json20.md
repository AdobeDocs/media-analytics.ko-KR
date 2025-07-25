---
title: Analytics 2.0 API를 사용하여 동시 뷰어 JSON 보고서 데이터 가져오기
description: Analytics 2.0 API를 사용하여 동시 뷰어 보고서 데이터를 가져오는 방법에 대해 알아봅니다. 요청 및 응답 샘플을 확인하십시오.
uuid: 9168f114-2459-4951-a06c-57b735d09dc0
exl-id: f84f63d3-b0d0-45fe-95a7-159f22d60660
feature: "Streaming Media, Workspace Basics"
role: User, Admin, Data Engineer
source-git-commit: 67f1fa8194fa58b2c513e3136d2bc7880f9cb06b
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 100%

---


# Analytics 2.0 API를 사용하여 동시 뷰어 JSON 보고서 데이터 가져오기{#get-concurrent-viewers-json-report-data}

[_*Analytics 2.0 API*_](https://www.adobe.io/apis/experiencecloud/analytics/docs.html)를 사용하여 동시 뷰어 보고서 데이터를 가져올 수 있습니다.

1. UI를 기반으로 구축된 세그먼트를 사용하여 데이터를 필터링합니다. 특정 콘텐츠 ID별로 필터링하려면 새 세그먼트를 만듭니다.
1. 요청 본문에서 `elements` -> `id`를 `metrics/concurrent_viewers_visitors`로 설정합니다.
1. 충분한 양의 데이터를 요청합니다.

   * 보고서에서 지정한 데이터 범위는 모든 동시 뷰어 데이터를 _비디오 세션이 종료된 시점에 수집합니다._
한 날 시작하여 자정 이후에(즉, 다음 날) 끝나는 세션을 고려해야 합니다.

   * 요청에서 의도한 기간에 하루 더 데이터를 요청하지만 분석에서 _*의도한 데이터만 사용합니다.*_

데이터 하루 동안의 샘플 요청 페이로드는 다음 샘플과 비슷합니다. 요청은 2일 연속으로 수행되지만 보고에서는 첫 번째 날만 사용합니다.

## 샘플 요청

```json
{
    "rsid": "[YOUR_RSID]",
    "locale": "en_US",
    "dimension": "variables/daterangeminute",
    "globalFilters": [
        {
            "dateRange": "2020-09-02T00:00/2020-09-03T00:00",
            "type": "dateRange"
        }
    ],
    "metricContainer": {
        "metrics": [
            {
                "columnId": "column1",
                "id": "metrics/concurrent_viewers_visitors"
            }
        ]
    },
    "settings": {
        "dimensionSort": "asc",
        "limit": "2000",
        "page": 0
  }
}
```

## 샘플 응답

```JSON
{
   "totalPages":1,
   "firstPage":true,
   "lastPage":true,
   "numberOfElements":1440,
   "number":0,
   "totalElements":1440,
   "columns":{
      "dimension":{
         "id":"variables/daterangeminute",
         "type":"time"
      },
      "columnIds":[
         "column1"
      ]
   },
   "rows":[
      {
         "itemId":"12008020000",
         "value":"00:00 2020-09-02",
         "data":[
            123.0
         ]
      },
      {
         "itemId":"12008020001",
         "value":"00:01 2020-09-02",
         "data":[
            143.0
         ]
      },
      {
         "itemId":"12008020002",
         "value":"00:02 2020-09-02",
         "data":[
            167.0
         ]
      },

      ...
      {
         "itemId":"12008022359",
         "value":"23:59 2020-09-02",
         "data":[
            768.0
         ]
      }
   ],
   "summaryData":{
      "filteredTotals":[
         17124.0
      ],
      "totals":[
         18453.0
      ]
   }
}
```


<!--
You can extract the concurrent viewers report data using the Experience Cloud API Explorer as follows.

1. Navigate to: [https://www.adobe.io.](https://www.adobe.io)
1. Select and enter the following information in the API Explorer form:

    * **API -** Select "Report".
    * **Method -** Select "Queue".
    * **Environment -** Select your data center.
    * Request JSON - Specify the following:

        * `reportSuiteID` - For info on reports suites: [Report Suites](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html?lang=ko)

        * `dateTo` - End date of the report.         

          >[!NOTE]
          >
          >The maximum time period supported is two days.

        * `dateFrom` - Start date of the report.
        * `elements : id` - Set to `"videoconcurrentviewers"`

        * `elements : top` - Specify the number of entries to be returned.

      Sample request body:

      ```    
      {
          "reportDescription": {
              "reportSuiteID": "[Your Report Suite ID]",
              "dateTo": "2017-09-07",
              "dateFrom": "2017-09-07"
              "metrics": [
                  {
                      "id": "instances"
                  }
              ],
              "elements": [
                  {
                      "id": "videoconcurrentviewers",
                      "top": 2880
                  }
              ]
              "locale": "en_US"
          }
      }

      ```

      >[!TIP]
      >
      >Some sessions are ended on the next day, and at that point the data will be available for reporting. In that case the best approach is to select 2 days (2880 minutes) of data, and use only the data for the first day (1440 minutes).

1. Click **Get Response**.

   In the Response field, you should get a `reportID`.
1. In the form, change **Method** to "Get".
1. Enter the value of the `reportID` you received in Step 3, and click **Get Response**.

   The concurrent viewers report data, in JSON format, is presented in the Response field.

   For example:

   ![](assets/api_helper_2.png)

   ![](assets/api_helper_1.png)

-->
