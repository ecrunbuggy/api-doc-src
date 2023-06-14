# Embedding iFrame Order Status

The flow consists of 3 main steps:

## 1) [Create an Order](https://runbuggy.stoplight.io/docs/shipping-api/b3A6NDE4MzU1MTY-create-an-order)

## 2) Receive JWT token
This token is used to share Status with Buyer / Seller

```bash
==== REQUEST ====
curl --location --request POST 'https://ng.runbuggy.com/testng/api/oauth2/token' \
--header 'Authorization: Bearer gq6ju4vov6hr7tkslkojm9imlinfn2te' \
--header 'Content-Type: application/json' \
--data-raw '{
    "scope":"openid"
}'

==== RESPONSE ====
{
    "access_token": "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJzeXN0ZW0uYmF0QGhveWVib3llLmNvbSIsInVzZXJJZCI6InN5c3RlbS5iYXRAaG95ZWJveWUuY29tIiwicmJ1c2VyIjp7InBhc3N3b3JkIjoiIiwidXNlcm5hbWUiOiJzeXN0ZW0uYmF0QGhveWVib3llLmNvbSIsImF1dGhvcml0aWVzIjpbeyJhdXRob3JpdHkiOiJST0xFX0FVQ1RJT05fSE9VU0UifV0sImFjY291bnROb25FeHBpcmVkIjp0cnVlLCJhY2NvdW50Tm9uTG9ja2VkIjp0cnVlLCJjcmVkZW50aWFsc05vbkV4cGlyZWQiOnRydWUsImFjY291bnRBY3RpdmF0aW9uU3RhdHVzIjp7ImlzQWNjb3VudEFjdGl2YXRlZCI6dHJ1ZSwiaXNBY2NvdW50VmVyaWZpZWQiOnRydWV9LCJhZGRpdGlvbmFsSW5mbyI6eyJhZGRyZXNzIjoiMTMwMCAxN3RoIFN0LCBTYW4gRnJhbmNpc2NvLCBDQSA5NDEwNywgVVNBIiwiYWRkcmVzc0lkIjoiNWNmODE4ZDRlNGIwMDFlOWIwMTBiNTljIiwiYnVzaW5lc3NBZGRyZXNzTGF0aXR1ZGUiOjM3Ljc2NTMxNjAwOTUyMTQ4LCJidXNpbmVzc0FkZHJlc3NMb25naXR1ZGUiOi0xMjIuMzk3MDU2NTc5NTg5OCwiY29tcGFueUlkIjoiNTE2MWExYzEtNTE1YS00NjFkLTlkODMtZDkyNGVlMDZiZWQxIiwiY29tcGFueU5hbWUiOiJicmluZ2F0cmFpbGVyIG1lZGlhIGxsYyIsImNvbnRhY3ROdW1iZXIiOiI1NTU1NTU1NTU1IiwiaXNWaW5sZXNzRW5hYmxlZCI6ZmFsc2UsImxhc3RDb21wbGV0ZWRQcm9maWxlU3RhdGUiOiJwcm9maWxlLmdvb2RTdGFuZGluZyIsInB1Ymxpc2hhYmxlS2V5IjoicGtfdGVzdF8wRzRTWEdXNUdNNDE3cHQ5UE9aUTBYSFciLCJyZWNvbmNpbGlhdGlvbkNvZGVzIjpudWxsLCJpc0NyZWF0b3IiOmZhbHNlfSwiY29udGFjdE5vIjoiNTU1NTU1NTU1NSIsImNyZWF0ZWREYXRlIjoxNjA4NzU5OTY2NDcyLCJlbWFpbFN1YnNjcmlwdGlvbnMiOnsiYmlsbE9mTGFkaW5nRHJvcHBlZFVwRW1haWwiOmZhbHNlLCJiaWxsT2ZMYWRpbmdQaWNrZWRVcEVtYWlsIjpmYWxzZSwiZXhwZWRpdGVkT3JkZXJQbGFjZWRFbWFpbCI6ZmFsc2UsIm5ld0NoYXRNZXNzYWdlRW1haWwiOmZhbHNlLCJvcmRlckF2YWlsYWJsZUVtYWlsIjpmYWxzZSwib3JkZXJDYW5jZWxsZWRFbWFpbCI6ZmFsc2UsIm9yZGVyQ2hhcmdlZEVtYWlsIjpmYWxzZSwib3JkZXJDbGFpbWVkRW1haWwiOmZhbHNlLCJvcmRlclBsYWNlZEVtYWlsIjpmYWxzZSwicGF5bWVudERlbGl2ZXJlZEVtYWlsIjpmYWxzZX0sImZpcnN0TmFtZSI6IlN5c3RlbSIsImhhc0NvbXBhbnlEZXRhaWxzIjp0cnVlLCJoYXNQYXltZW50RGV0YWlscyI6dHJ1ZSwiaGFzVXNlclByb2ZpbGVEZXRhaWxzIjp0cnVlLCJpc1RlbXBvcmFyeVBhc3N3b3JkU2V0IjpmYWxzZSwiaXNVc2VyQWN0aXZlQW5kTm90VW5zdWJzY3JpYmVkRW1haWwiOnRydWUsImxhc3RDb21wbGV0ZWRQcm9maWxlU3RhdGUiOiJwcm9maWxlLmdvb2RTdGFuZGluZyIsImxhc3ROYW1lIjoiQnJpbmdBVHJhaWxlciIsInNtc1N1YnNjcmliZWQiOmZhbHNlLCJ1c2VySWQiOjE1NTk2LCJpbnRlcmNvbV91c2VyX2hhc2giOiI3YjY3ZTMxY2Q2MzI3ODBlODYyNzcyNzA4ZWJkODIwMzQxMWVmZTJjODljNzg2MGY3ODFmOGM4NThmZDhmYTc0In0sImV4cCI6MTYwODc2MjcxOX0.fPMwRwzBHcrxcCYBvMrObAq-dC3hULjnnUGpVGvky2c",
    "expires_in": 60,
    "scope": "openid"
}
```

## 3) Open Order Status in IFrame

The IFrame URL is constructed out of 4 query parameters:

 - `orderId` *(required)* The order you want to show the order status for.
 - `token`  *(required)*  The JWT token received from **Step 3**
 - `statusWhitelist` *(optional)* A comma separated list of statuses. This list determines which statuses to show 
   on the status bar and in the timeline. If omitted all statuses will be displayed.
     - *Statuses supported:* AVAILABLE, ORDER_NOTIFICATIONS, CLAIMED, VEHICLES_PICKEDUP, VEHICLES_SIGNATURE_PICKEDUP, 
       UNLOADED, VEHICLES_DELIVERED, VEHICLES_SIGNATURE_DELIVERED, COMPLETED
 - `sections` *(required)* A comma separated list of sections to show in the IFrame.
     - *Options:* MAP, STATUS_BAR, TIMELINE

The final embeddable URL would look like:

https://apps.runbuggy.com/runbuggy/spa-v2/#/external/order-status?orderId=<ORDER ID>&token=<RESPONSE 3 TOKEN>&sections=<COMMA SEPARATED SECTIONS TO SHOW>&statusWhitelist=<COMMA SEPARATED STATUSES>

### Sections Overview
#### Map

A map with order details

![Map](https://runbuggyinc.github.io/api-doc-src/shippers/assets/widget-map.png)

#### Status Bar

A status bar showing the progression of the order. The statuses can be whitelisted using the `statusWhitelist` parameter

![Status Bar](https://runbuggyinc.github.io/api-doc-src/shippers/assets/widget-status-bar.png)

#### Timeline

A timestamped chronological list of order statuses. The statuses can be whitelisted using the `statusWhitelist` parameter

![Timeline](https://runbuggyinc.github.io/api-doc-src/shippers/assets/widget-timeline.png)
