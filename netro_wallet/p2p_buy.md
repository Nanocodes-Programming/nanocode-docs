# P2p buy flow documentation 

## Get details of a p2p ad

**Endpoint:** `/p2p/ad/detail/{id}`  
**Method:** `GET`  
**Permissions:** IsAuthenticated  

### Responses:
**200 ok:** Category added successfully.
```json
  {
  "status": "success",
  "entity": {
    "id": 1,
    "user": {
      "id": "598b1f02-b6b5-4197-a399-c8537e45d768",
      "ratings": {
        "positive_feedback_count": 4,
        "negative_feedback_count": 0,
        "averate_rating": 4.5
      },
      "password": "pbkdf2_sha256$720000$K3Bsv9j88nIs3KtPKNsy3H$//bxOtNmXe92IDJQfYGocd8CNhHfRPKo0m0aVlqFIWo=",
      "last_login": "2024-10-05T06:43:40.653113+01:00",
      "email": "onuhudoudo@gmail.com",
      "email_verified": true,
      "phone_number_verified": false,
      "country_verified": false,
      "google_id": null,
      "facebook_id": null,
      "phone_number": null,
      "is_staff": false,
      "is_superuser": false,
      "is_active": true,
      "two_factor_enabled": false,
      "two_factor_type": "email",
      "created_at": "2024-09-16T10:13:32.027738+01:00",
      "updated_at": "2024-10-05T06:49:22.870974+01:00",
      "fullname": "Kyrian",
      "country": null,
      "transaction_id": 9,
      "has_kyc": false,
      "has_p2p": true,
      "is_banned": false,
      "groups": [],
      "user_permissions": []
    },
    "crypto_currency": "trx",
    "price_per_unit": "10000.00",
    "ad_type": "buy",
    "payment_method": "bank_transfer",
    "fiat_currency": "usd",
    "crypto_amount": "10000.00000000000000000000",
    "start_date": "2024-09-23",
    "end_date": "2024-09-23",
    "auto_reply_message": "string",
    "terms_of_trade": "string",
    "additional_information": "string",
    "status": "pending",
    "max_limit": "60000.0000000000",
    "min_limit": "3000.0000000000",
    "total_available": "100000.0000000000",
    "trade_started_at": "2024-09-24T12:20:37.699577+01:00",
    "trade_completed_at": null,
    "asset_id": null,
    "time_to_pay": 3
  },
  "message": null,
  "success": true
}



**401 unauthorized:**  User is not logged in.
```json
 {
  "detail": "Authentication credentials were not provided."
}
```






## Create an offer

An offer signals to the seller that a buyer is interested in trading with them through a P2P transaction, this endpoint sends an email to the seller showcasing the buyers proposal 

**Endpoint:** `/p2p/offer/create/`  
**Method:** `POST`  
**Permissions:** IsAuthenticated 

### Responses:
**200 OK:** Offer created.
```json
{
  "status": "success",
  "entity": {
    "id": 9,
    "created_at": "2024-10-07T10:07:00.847278+01:00",
    "currency_amount": "10.00000000000000000000",
    "status": "pending",
    "fiat_amount": "2000.00",
    "has_indicated_paid": false,
    "ad": 1,
    "user": "a0f4b68d-90b9-4aaf-82e5-4c500f702fb1"
  },
  "message": "Offer created successfully",
  "success": true
}
```

**400 Bad reqeust:** An error occured as described by the message field.
```json 
{
  "status": "failure",
  "entity": null,
  "message": "(ad) Invalid pk \"0\" - object does not exist.",
  "success": false
}
```




## Indicate payment on an offer

This endpoint sends an email to the seller indicating a buyer claims to have made payment 

**Endpoint:** `/p2p/offer/paid/{id}/`  
**Method:** `POST`  
**Permissions:** IsAuthenticated 

### Params
**Id:** The id of the offer


### Responses:
**200 OK:** Success
```json
{
  "status": "success",
  "entity": null,
  "message": "Offer successfully marked as paid",
  "success": true
}
```

**400 Bad reqeust:** An error occured as described by the message field.
```json 
{
  "status": "failure",
  "entity": null,
  "message": "Offer has already been marked as paid",
  "success": false
}
```

```json
{
  "status": "failure",
  "entity": null,
  "message": "You are not authorized to indicate payment on this offer",
  "success": false
}
``` 





## Cancel an offer

This endpoint sends an email to the seller indicating a buyer has cancelled their interest and the ad is now open to new offers

**Endpoint:** `/p2p/offer/cancel/{id}/`  
**Method:** `POST`  
**Permissions:** IsAuthenticated 

### Params
**Id:** The id of the offer


### Responses:
**200 OK:** Success
```json
{
  "status": "success",
  "entity": null,
  "message": "Offer cancelled successfully",
  "success": true
}
```

**400 Bad reqeust:** An error occured as described by the message field.

```json 
{
  "status": "failure",
  "entity": null,
  "message": "This offer is already cancelled",
  "success": false
}
```
```json
{
  "status": "failure",
  "entity": null,
  "message": "You are not authorized to cancel this offer",
  "success": false
}
``` 





## Release funds to buyer 

This endpoint releases the funds (total_available) to the buyer, it sends an email to the buyer and also dispatches a websocket action which is recieived buy the buyer if they are logged in and connected to the p2p websocket route

**Endpoint:** `/p2p/offer/release/{id}/`  
**Method:** `POST`  
**Permissions:** IsAuthenticated 

### Params
**Id:** The id of the offer

### Responses:
**200 OK:** Success
```json
{
  "status": "success",
  "entity": null,
  "message": "Funds have been released successfully",
  "success": true
}
```

**400 Bad reqeust:** An error occured as described by the message field.

```json 
{
  "status": "failure",
  "entity": null,
  "message": "Offer not found",
  "success": false
}
```
Offer was not found 


```json 
{
  "status": "failure",
  "entity": null,
  "message": "You are not authorized to release funds on this trade",
  "success": false
}
```
The logged in user is not the owner of the ad 


```json 
{
  "status": "failure",
  "entity": null,
  "message": "Offer is already cancelled",
  "success": false
}
```
You can only cancel a pending offer





## Listening for real time messages from the websocket

When a seller releases the assets to a buyer, an email is sent to notify the buyesr of the completed transaction, a websocket action is also dispatched to the buyer if they are logged in and connected to the websocket 


### websocket route 

`/ws/p2p/?token={user_access_token}`

When the funds is released, the buyer gets the following message through the websocket

```json 
{
    "message": "Funds have been released",
    "amount": 100000.0,
    "type": "funds_released",
    "crypto_currency": "trx"
}
```

When an offer is created for an ad, the following message is sent to the seller through websocket 

```json 
{
    "message": "You have an interested buyer on your p2p ad",
    "type": "ad_interest",
    "ad_id": 2,
    "offer_id": 12
}
```


When an offer is cancelled by the buyer the following message is sent to the seller through websocket 

```json 
{
    "message": "Kyrian has cancelled their offer regarding your P2P advertisement.",
    "type": "offer_cancel",
    "offer_id": 12
}
```

When the buyer indicates payment on an offer, the following message is sent to the seller throught the websocket 

```json 
{
    "message": "Kyrian has claimed to have made payment regarding your P2P advertisement.",
    "type": "payment_indication",
    "offer_id": 12
}
```



