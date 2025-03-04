---
nav_title: "GET: Export Revenue Data"
article_title: "GET: Export Revenue Data"
search_tag: Endpoint
page_order: 2
layout: api_page
page_type: reference
description: "This article outlines details about the Export revenue data Braze endpoint."

---
{% api %}
# Export revenue data by time
{% apimethod get %}
/purchases/revenue_series
{% endapimethod %}

> Use this endpoint to return the total money spent in your app over a time range.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#f6e05f9a-13c0-4d66-8caa-4a376d25749f{% endapiref %}

## Rate limit

{% multi_lang_include rate_limits.md endpoint='purchases product list' %}

## Request parameters

| Parameter | Required | Data Type | Description |
|---|---|---|---|
| `ending_at` | Optional | Datetime ([ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) string) | Date on which the data export should end. Defaults to time of the request. |
| `length` | Required | Integer | Maximum number of days before `ending_at` to include in the returned series. Must be between 1 and 100 (inclusive). |
| `unit` | Optional | String | Unit of time between data points. Can be day or hour, defaults to day. |
| `app_id` | Optional | String | App API identifier retrieved from the [API Keys]({{site.baseurl}}/user_guide/administrative/app_settings/api_settings_tab/) page. If excluded, results for all apps in a workspace will be returned. |
| `product` | Optional | String | Name of product to filter response by. If excluded, results for all apps will be returned. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Example request

```
curl --location --request GET 'https://rest.iad-01.braze.com/purchases/revenue_series?length=100' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```

## Response

```json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "message": (required, string) the status of the export, returns 'success' when completed without errors,
  "data" : [
    {
      "time" : (string) the date as ISO 8601 date,
      "revenue" : (int) amount of revenue for the time period
      },
    ...
  ]
}
```

{% endapi %}

{% alert tip %}
For help with CSV and API exports, visit [Export troubleshooting]({{site.baseurl}}/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).
{% endalert %}
