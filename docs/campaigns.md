# Campaigns

## One For Free
The "free" campaign is a promotional offer that rewards customers with a complimentary product after they have purchased a specified number of items. For every qualifying purchase within the campaign, customers earn a point or a "stamp" on a digital loyalty card. Upon accumulating enough points to meet the predetermined threshold, the customer is eligible to receive a free product, at which point the current loyalty card is considered redeemed. Subsequently, a new digital loyalty card is issued, allowing the customer to start accumulating points anew with each subsequent purchase of the eligible products.

### Campaign Data Model Overview
The campaign data model allows merchants to customize a variety of rules and settings. This document focuses specifically on the options available for the "free" campaign type, highlighting three key parameters: <span style="color: teal;">**type**</span>, <span style="color: teal;">**triggerAmount**</span>, and <span style="color: teal;">**aggregateMode**</span>, as illustrated in the example JSON provided below.

#### type
The "One For Free" campaign is internally designated as "free". This identifier must be used precisely as shown, including case sensitivity, to ensure proper configuration.

#### triggerAmount
This parameter sets the threshold for activating the campaign. It requires an integer value of minimum 2, with 10 being a typical setting. The triggerAmount determines the number of purchases needed for a customer to qualify for a free product.

#### aggregateMode
This setting dictates the manner in which customer points are accumulated across specific products within the campaign, such as product A and B. Points are awarded per product purchase, impacting how the free product is earned.  Legal values are <span style="color: teal;">**all**</span> and <span style="color: teal;">**individual**</span>.

##### all
In the "all" mode, points from purchases of all relevant products are aggregated. For a campaign with a triggerAmount of 10, customers can mix and match products A and B in any combination that totals 10 to qualify. The customer will be charged for 9 items and receive the least expensive of the two (A or B) for free.

##### individual
The "individual" mode requires customers to accumulate points on a per-product basis. For example, with a triggerAmount of 10, a customer must purchase 10 of product A to receive the tenth product A for free, effectively paying for only 9.

This model offers a versatile approach to structuring campaigns, enabling customized promotional strategies that cater to diverse purchasing habits and preferences. For instance, imagine you own a coffee shop and wish to launch a loyalty program for your customers. You could introduce a scheme where "a coffee is a coffee," indicating that regardless of the size, type, or price of the coffee purchased, customers are entitled to their 10th coffee for free. With this strategy, you would set the aggregateMode to "all" allowing for a unified treatment of all coffee purchases under the loyalty program.

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
The customer loyalty data model is designed to capture and represent the points a customer accumulates through participation in various loyalty campaigns. This model enables tracking of points earned on multiple products within individual campaigns, as well as the ability to accumulate points across different campaigns concurrently. The JSON example below illustrates how customer loyalty information is structured, focusing specifically on the loyaltyCampaigns section.

Key features of the loyaltyCampaigns section include:

- **Multiple Campaign Participation**: Customers can be active in more than one loyalty campaign at a time, allowing for diverse avenues of engagement and reward accumulation.
- **Product-Specific Points**: Within each campaign, points are tracked on a per-product basis. This granularity supports tailored rewards that reflect the customer's specific purchasing behaviors.
- **Campaign and Item Identification**: Each loyalty campaign and associated product is uniquely identified (via campaignId and itemId), ensuring precise tracking and attribution of earned points.
- **Point Accumulation**: The model captures the number of points earned for each product (earned), offering a clear view of the customer's progress towards reward thresholds.

``` JSON title="Sample Customer Data Model" hl_lines="12-37"
{
  "customerId": "a9f62394-13ed-43e0-9baf-4a60223304da",
  "displayName": "John Doe",
  "isCreditAllowed": true,
  "privateCustomer": {
    "firstName": "John",
    "lastName": "Doe",
    "mobilePhone": "123-45-97890",
    "email": "johndoe@example.com",
    "isCustomerClubMember": true,
    "customerClubMember": {},
    "loyaltyCampaigns": [
      {
        "campaignId": "7cf8f7ea-f7cc-4800-8ccc-6ee868781e35",
        "type": "free",
        "loyaltyItems": [
          {
            "itemId": "e593f5c4-6474-4d0b-a20d-c4de6d483bbc",
            "earned": 7
          }
        ]
      },
      {
        "campaignId": "9f06f0a2-26c3-4e67-ae8d-e68d7849303a",
        "type": "free",
        "loyaltyItems": [
          {
            "itemId": "64e5ed48-4893-4502-bf51-c6b9ae593b80",
            "earned": 6
          },
          {
            "itemId": "15bf8efc-4202-4214-a567-25ca722bc784",
            "earned": 3
          }
        ]
      }
    ]
  },
  "displayNameCalculated": "John Doe"
}
```

