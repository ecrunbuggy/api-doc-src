# Vehicle Request Requirements
When [creating an order](/docs/shipping-api/b3A6NDE4MzU1MTY-create-an-order), you have two options for sending over the vehicle information.

## Provide the VIN
*example*:
```json
//example from Create Order request
{
  "vehicleTransferOrders": [
   {
      "vehicle": {
        "vin": "1N4BA42E55C836454"
      }
   }
  ]
}
```

## Provide the Vehicle details, VIN will be ignored
```json
//example from Create Order request
{
  "vehicleTransferOrders": [
   {
      "vehicle": {
        "year": "1969",
        "make": "Chevrolet",
        "model": "Corvette"
      }
   }
  ]
}
```