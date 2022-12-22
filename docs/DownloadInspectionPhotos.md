---
stoplight-id: misvonsl6wjxs
---

# Pulling Inspection Photos Via API

​1. Use the full request to get the pickup and dropoff ids.

[API Docs reference](https://docs.runbuggy.com/docs/shipping-api/e37c8f68eee73-retrieve-an-expanded-order)​

```raw
curl 'https://ng-staging.runbuggy.com/staging/api/orders/{id}/full' \
-X 'GET' \
-H 'Accept: application/json, text/plain, */*' \
-H 'Authorization: TOKEN GOES HERE' \
```

In the response you will need the _VTO id_, _pickup id_ and the _dropoff id_. see below examples

### example of VTO id in json response

```raw
"vehicleTransferOrders": [
        {
            "id": "8da9da90-477a-43b0-adcf-ee22764556ed",
```

### example of _pickup_ inspection id in json response

```raw
	 "inspections": [
                {
                    "id": "62a24b3ffe23b617ba3a402e",
                    "taskName": "PICKUP_INSPECTION",
```

### example of _dropoff_ inspection id in json response

```raw
{
"id": "62a27e1c4b53ba0de0337668",
"taskName": "DROPOFF_INSPECTION",
}
```

## 2. Use the inspection endpoint to get the image resources. 

Each resource has an id. This is what is needed to pull the images. See examples below:

### Pick up address

```raw
curl 'https://ng-staging.runbuggy.com/staging/api/vehicle-transfer-orders/{{VTO ID}}/inspections/{{INSPECTION ID}}' \
-X 'GET' \
-H 'Accept: application/json, text/plain, */*' \
-H 'Pragma: no-cache' \
-H 'Authorization: TOKEN HERE' \
-H 'Referer: https://apps.runbuggy.com/runbuggy/spa-v2/' \
-H 'Cache-Control: no-cache' \
-H 'Host: apps.runbuggy.com' \
-H 'Accept-Language: en-GB,en;q=0.9' \
-H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.5 Safari/605.1.15' \
-H 'Accept-Encoding: gzip, deflate, br' \
-H 'Connection: keep-alive'
```

### Dropoff address

```raw
curl 'https://ng-staging.runbuggy.com/staging/api/vehicle-transfer-orders/{{VTO ID}}/inspections/{{INSPECTION ID}}' \
-X 'GET' \
-H 'Accept: application/json, text/plain, */*' \
-H 'Pragma: no-cache' \
-H 'Authorization: TOKEN HERE' \
-H 'Referer: https://apps.runbuggy.com/runbuggy/spa-v2/' \
-H 'Cache-Control: no-cache' \
-H 'Host: apps.runbuggy.com' \
-H 'Accept-Language: en-GB,en;q=0.9' \
-H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.5 Safari/605.1.15' \
-H 'Accept-Encoding: gzip, deflate, br' \
-H 'Connection: keep-alive'
```

With each response the the image id is located in the _inspectionPoints_ array in the json response . example of image id in json response

```raw
 {
            "name": "ODOMETER",
            "description": "Odometer Image",
            "isMandatory": true,
            "comments": "",
            "images": [
                {
                    "id": "7ec63ba0-e849-11ec-87e6-e947b6d1a01c",
```

## 3. To download the image, use the endpoint below:

```raw
curl 'https://ng-staging.runbuggy.com/staging/api/vehicle-transfer-orders/{{VTO ID}}/photos/{{IMAGE ID}}/hd' \
-X 'GET' \
-H 'Accept: */*' \
-H 'Pragma: no-cache' \
-H 'Authorization: TOKEN HERE' \
-H 'Referer: https://apps.runbuggy.com/runbuggy/spa-v2/' \
-H 'Cache-Control: no-cache' \
-H 'Host: apps.runbuggy.com' \
-H 'Accept-Language: en-GB,en;q=0.9' \
-H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.5 Safari/605.1.15' \
-H 'Accept-Encoding: gzip, deflate, br' \
-H 'Connection: keep-alive'
```