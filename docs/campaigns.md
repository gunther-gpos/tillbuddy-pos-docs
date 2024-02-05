# Campaigns

## One For Free
The "free" campaign is a promotional offer that rewards customers with a complimentary product after they have purchased a specified number of items. For every qualifying purchase within the campaign, customers earn a point or a "stamp" on a digital loyalty card. Upon accumulating enough points to meet the predetermined threshold, the customer is eligible to receive a free product, at which point the current loyalty card is considered redeemed. Subsequently, a new digital loyalty card is issued, allowing the customer to start accumulating points anew with each subsequent purchase of the eligible products.

### Campaign Data Model Overview
The campaign data model allows merchants to customize a variety of rules and settings. This document focuses specifically on the options available for the "free" campaign type, highlighting three key parameters: <span style="color: teal;">**type**</span>, <span style="color: teal;">**triggerAmount**</span>, and <span style="color: teal;">**aggregateMode**</span>, as illustrated in the example JSON provided below.

#### type
The "One For Free" campaign is internally designated as "free". This identifier must be used precisely as shown, including case sensitivity, to ensure proper configuration.

#### triggerAmount
This parameter sets the threshold for activating the campaign. It requires an integer value greater than 0, with 10 being a typical setting. The triggerAmount determines the number of purchases needed for a customer to qualify for a free product.

#### aggregateMode
This setting dictates the manner in which customer points are accumulated across specific products within the campaign, such as product A and B. Points are awarded per product purchase, impacting how the free product is earned.  Legal values are <span style="color: teal;">**all**</span> and <span style="color: teal;">**individual**</span>.

##### all
In the "all" mode, points from purchases of all relevant products are aggregated. For a campaign with a triggerAmount of 10, customers can mix and match products A and B in any combination that totals 10 to qualify. The customer will be charged for 9 items and receive the least expensive of the two (A or B) for free.

##### individual
The "individual" mode requires customers to accumulate points on a per-product basis. For example, with a triggerAmount of 10, a customer must purchase 10 of product A to receive the tenth product A for free, effectively paying for only 9.

This model provides flexibility in how campaigns are structured, allowing for tailored promotional strategies that can accommodate different purchasing behaviors and preferences.


``` JSON title="Sample Campaign Data Model" hl_lines="11 13 14 15 16"
{
  "campaignId": "7cf8f7ea-f7cc-4800-8ccc-6ee868781e35",
  "companyId": "e18aa87a-a1f5-4b78-89af-b3fd2a76406c",
  "storeId": "e18aa87a-a1f5-4b78-89af-b3fd2a76406c",
  "name": "Kaffeavtalen",
  "summary": "",
  "receipt": {
    "text": "Kaffedeal"
  },
  "priority": 1,
  "type": "free",
  "typeValue": "",
  "freeCampaignDetails": {
    "triggerAmount": 10,
    "aggregateMode": "all"
  },
  "impactAll": false,
  "allowMix": false,
  "isValidOnlyForLoyaltyClub": false,
  "effectiveFrom": "2024-01-19T12:00:00.000Z",
  "endingAt": "2024-03-19T12:00:00.000Z",
  "products": [
    {
      "productId": "e593f5c4-6474-4d0b-a20d-c4de6d483bbc",
      "displayName": "Kaffe mocca enkel"
    },
    {
      "productId": "2a7402c3-5629-49ab-9bd1-adba270acf32",
      "displayName": "Kaffe mocca dobbel - Kafé inne"
    },
    {
      "productId": "e63a1499-4439-462c-94ed-e12b2dea8d55",
      "displayName": "Kakao - het chili"
    }
  ],
  "brands": [],
  "categories": [],
  "lastModifiedAt": "2024-01-18T08:00:00"
}
```
### Customer Data Model Overview