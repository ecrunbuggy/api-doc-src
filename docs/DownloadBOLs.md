---
stoplight-id: jfj2qs9nubq5a
---

# Downloading Bills of Lading

Get the full RunBuggy order details. Replace the text in curly brackets in the URL with your order ID.

[Retrieve an Expanded Order](https://docs.runbuggy.com/docs/shipping-api/e37c8f68eee73-retrieve-an-expanded-order)

```plaintext
curl --location --request GET 'https://apps.runbuggy.com/v2/api/orders/{{ORDERID}}/full' \
--header 'Authorization: Bearer CHANGEME' \
--data-raw ''
```

The JSON response will contain a root-level key `"transportationOrders"`. Iterate through each transportation order to get the transportation order `"id"` and `"billsOfLading"`.

The billsOfLading list will contain the BOLs for that transportation order. Iterate the BOLs to retrieve each BOL `"id"`.

An example response is below with the pertinent information. An actual response would show more information.

```json
{
  "id": "d86cd3d6-bb54-4feb-b48d-f4cb395e1bea",
  "referenceNumber": "S-007630860",
  "type": "BASIC",
  "transportationOrders": [
    {
      "id": "08ac661b-105a-4ce5-a4a6-47fe06529847",
      "referenceNumber": "T-006634754",
      "type": "BASIC",
      "vehicleTransferOrders": [
        {
          "id": "ececc401-4042-4957-b9dc-cbb7ab71548a"
        }
      ],
      "billsOfLading": [
        {
          "id": "06021337-7d40-4bc6-9d91-7326d370d713",
          "createdAt": "2022-12-01T16:06:13.212",
          "updatedAt": "2022-12-01T16:13:48.045",
          "document": "order-workflow-staging/transportationOrder/08ac661b-105a-4ce5-a4a6-47fe06529847/06021337-7d40-4bc6-9d91-7326d370d713/bol",
          "data": {
            "payer": {
              "id": "a702e55f-8da8-4dbf-896a-b8d643d712bc",
              "name": "RB Dealer",
              "type": "SHIPPER"
            },
            "transporter": {
              "id": "895aad3b-390c-4f2b-90f9-cba1e77ad472",
              "name": "Phillip Quality Car Shippers LLC"
            },
            "paymentMethod": null,
            "transportationOrderReferenceNumber": "T-006634754",
            "transportationOrderNotes": "",
            "pickupAddress": "1473 Castillion Dr NE, Warren, OH 44484, USA",
            "driverPickupNotes": null,
            "pickupDate": "2022-12-01T16:09:41.684+00:00",
            "dropoffAddress": "200 W Monroe St, Phoenix, AZ 85003, USA",
            "driverDropoffNotes": null,
            "dropoffDate": "2022-12-01T16:13:25.965+00:00",
            "distanceInMiles": 2048,
            "transportationCompanyAddress": null,
            "driverFullName": "Bryan Boye",
            "vehicles": [
              {
                "type": "Car",
                "year": 2012,
                "make": "Audi",
                "model": "A7",
                "isOverSized": false,
                "isOperational": true,
                "odometer": 0,
                "vehicleMeasurements": {
                  "height": 55.9,
                  "length": 195.6,
                  "width": 84.2,
                  "curbWeight": 4210.0,
                  "grossVehicleWeightRating": null,
                  "grossVehicleWeightRangeMin": null,
                  "grossVehicleWeightRangeMax": null,
                  "tonnage": null
                },
                "vehicleMarket": "LIGHT",
                "vin": "WAUYGAFC6CN174200",
                "rolls": true,
                "missingKeys": false
              }
            ]
          },
          "pickupSignature": "order-workflow-staging/transportationOrder/08ac661b-105a-4ce5-a4a6-47fe06529847/06021337-7d40-4bc6-9d91-7326d370d713/pickupSignature",
          "pickupDriversSignature": "order-workflow-staging/transportationOrder/08ac661b-105a-4ce5-a4a6-47fe06529847/06021337-7d40-4bc6-9d91-7326d370d713/pickupDriversSignature",
          "pickupSignedBy": "John",
          "pickupSignedAt": {
            "type": "Point",
            "coordinates": [null, null]
          },
          "dropoffSignature": "order-workflow-staging/transportationOrder/08ac661b-105a-4ce5-a4a6-47fe06529847/06021337-7d40-4bc6-9d91-7326d370d713/dropoffSignature",
          "dropoffDriversSignature": "order-workflow-staging/transportationOrder/08ac661b-105a-4ce5-a4a6-47fe06529847/06021337-7d40-4bc6-9d91-7326d370d713/dropoffDriversSignature",
          "dropoffSignedBy": "Jill",
          "dropoffSignedAt": {
            "type": "Point",
            "coordinates": [null, null]
          }
        }
      ]
    }
  ]
}
```

To get the RunBuggy PDF of the Bill of Lading, make the following request for each BOL ID and Transportation Order ID retrieved. Replace the items in curl brackets with the respective IDs. Using the example above, the Transportation Order ID would be `08ac661b-105a-4ce5-a4a6-47fe06529847` and the BOL ID would be `06021337-7d40-4bc6-9d91-7326d370d713`.

```plaintext
curl --location -g --request GET
'https://apps.runbuggy.com/runbuggy/orders-workflow/transportation-orders/{TRANSPORTATION ORDER ID}/bills-of-lading/{BOL ID}'
--header 'Authorization: Bearer CHANGEME' \
--data-raw ''
```

To save the BOL data to your own system, or to construct your own BOL document from the BOL data, any fields found in the order details JSON response can be used, such as:

-   pickupAddress
-   dropoffAddress
-   payer
-   transporter
-   pickupSignedBy
-   pickupSignedAt
-   dropoffSignedBy
-   dropoffSignedAt

          
