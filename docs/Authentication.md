# Authentication

A user interface for generating your API token will be in a future release. For now, your RunBuggy Account Representative or Sales Engineer can generate an API token for you, or you can reference the below instructions to generate your own.

-   Login to your account at <https://apps.runbuggy.com/> for the production environment, or <https://ng-staging.runbuggy.com/staging/spa-v2/#/login> for the staging environment.

![image.png](../assets/images/image.png)

-   Enter email address of your user and click continue.

-   A password-less login link will be sent via email to the address provided. Click on the link in the e-mail received, which will log you into the device from which the link was clicked.

-   Once logged-in, obtain your account's JWT token from the **Request Headers **value ‘Authorization’ in developer tools in your browser. The token can also be found in other requests in Network Tools, like the "devices" request.

![Screenshot_2.png](../assets/images/Screenshot_2.png)

-   Use this temporary JWT token to retrieve your long-lasting token from the API. Change the text "CHANGEME-JWTTOKEN" to the JWT token retrieved from the web interface.

Production environment curl:

```plaintext
curl --location --request POST 'https://apps.runbuggy.com/runbuggy/accounts/api-token/tokens' \
--header 'Authorization: Bearer CHANGEME-JWTTOKEN' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "My token",
  "description": "Token description",
  "disabled": false,
  "expireAt": null
}'
```

Staging environment curl:

```plaintext
curl --location --request POST 'https://ng-staging.runbuggy.com/staging/accounts/api-token/tokens' \
--header 'Authorization: Bearer CHANGEME' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "My token",
  "description": "Token description",
  "disabled": false,
  "expireAt": null
}'
```

-   Use the long-lasting token returned in the JSON response body for all following requests.

-   Add to HTTP header e.g. `Authorization: Bearer e8ujql7desph6bm4ajf6pop96mhevi39`

Example secure request:
```
curl --request POST \
  --url https://ng-staging.runbuggy.com/staging/api/orders \
  --header 'authorization: Bearer tfep1l767r0tolbln9f2apbalfamd2ok' \
  --header 'content-type: application/json' \ 
  --data '{}'
```
