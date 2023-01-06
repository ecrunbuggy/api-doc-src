# Downloading Bills of Lading

Get the full RunBuggy order details: [Retrieve an Expanded Order](https://docs.runbuggy.com/docs/shipping-api/e37c8f68eee73-retrieve-an-expanded-order)

The JSON response will contain a root-level key `"transportationOrders"`. Iterate through each transportation order to get the transportation order `"id"` and `"billsOfLading"`.

The billsOfLading list will contain the BOLs for that transportation order. Iterate the BOLs to retrieve each BOL `"id"`.

An example response is below with the pertinent information. An actual response would show more information.

```json
{
  "id": "d86cd3d6-bb54-4feb-b48d-f4cb395e1bea",
  "referenceNumber": "S-007630860",
  "transportationOrders": [
    {
      "id": "08ac661b-105a-4ce5-a4a6-47fe06529847",
      "referenceNumber": "T-006634754",
      "vehicleTransferOrders": [
        {
          "id": "ececc401-4042-4957-b9dc-cbb7ab71548a"
        }
      ],
      "billsOfLading": [
        {
          "id": "06021337-7d40-4bc6-9d91-7326d370d713",
        }
      ]
    }
  ]
}
```

To get the RunBuggy PDF of the Bill of Lading, make the following request for each BOL ID and Transportation Order ID retrieved. Replace the items in curly brackets with the respective IDs. Using the example above, the Transportation Order ID would be `08ac661b-105a-4ce5-a4a6-47fe06529847` and the BOL ID would be `06021337-7d40-4bc6-9d91-7326d370d713`.

```plaintext
curl --location -g --request GET
'https://apps.runbuggy.com/runbuggy/orders-workflow/transportation-orders/{TRANSPORTATION ORDER ID}/bills-of-lading/{BOL ID}'
--header 'Authorization: Bearer CHANGEME' \
--data-raw ''
```

## BOL Data
To save the BOL data to your own system, or to construct your own BOL document from the BOL data, any fields found in the order details JSON response can be used, such as:

-   pickupAddress
-   dropoffAddress
-   payer
-   transporter
-   pickupSignedBy
-   pickupSignedAt
-   dropoffSignedBy
-   dropoffSignedAt

          
