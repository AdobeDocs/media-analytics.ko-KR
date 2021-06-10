---
title: Concurrent Viewer JSON 보고서 데이터 가져오기
description: Concurrent Viewer JSON 보고서 데이터 가져오기
uuid: 9168f114-2459-4951-a06c-57b735d09dc0
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: ht
source-wordcount: '164'
ht-degree: 100%

---


# Concurrent Viewer JSON 보고서 데이터 가져오기{#get-concurrent-viewers-json-report-data}

Analytics API의 _*1.4 버전*_&#x200B;을 사용하여 동시 뷰어 보고서 데이터를 가져올 수 있습니다.
* [Analytics API](https://github.com/AdobeDocs/analytics-1.4-apis)
* [Swagger](https://adobedocs.github.io/analytics-1.4-apis/swagger-docs.html#/Report/Report.Get)

1. UI를 기반으로 구축된 세그먼트를 사용하여 데이터를 필터링합니다. 특정 콘텐츠 ID별로 필터링하려면 새 세그먼트를 만듭니다.
1. 요청 본문에서 `elements` -> `id`를 `videoconcurrentviewers`로 설정합니다.
1. 충분한 양의 데이터를 요청합니다. 데이터에 간격이 없도록 3200개의 데이터 포인트가 권장됩니다.

   * 보고서에서 지정한 데이터 범위는 모든 동시 뷰어 데이터를 _비디오 세션이 종료된 시점에 수집합니다._
따라서 한 날 시작하여 자정 이후에(즉, 다음 날) 끝나는 세션을 고려해야 합니다.

   * 하루 이상의 데이터를 요청하지만 분석에서는 _*첫 날의 데이터만 사용합니다.*_

이 시나리오에 대한 샘플 요청 페이로드는 다음과 같습니다.

```
{
  "reportDescription":{
    "reportSuiteID":"[YOUR_RSID]",
    "dateFrom":"2018-07-01",
    "dateTo":"2018-07-02",
    "metrics":[
      {
        "id":"instances"
      }
    ],
    "elements":[
      {
        "id":"videoconcurrentviewers",
        "top":"3200"
      }
    ],
    "segments":[
      {
        "id":"s1234_58ca4fc7e4b0abc238707bb9"                                         
      }
    ],
    "sortBy":"instances",
    "locale":"en_US"
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

        * `reportSuiteID` - For info on reports suites: [Report Suites](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html)
        
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
