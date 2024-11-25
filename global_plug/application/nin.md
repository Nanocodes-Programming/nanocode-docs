## Apply for a Nigerian NIN

**Endpoint:** `/nin/apply/`  
**Method:** `POST`  
**Permissions:** IsAuthenticated

**Request body:**

```json
{
  "email_address": "user@example.com",
  "preferred_date_of_appointment": "2024-11-15",
  "appointment_time": "00:00",
  "bvn": "11111111111",
  "title": "miss",
  "surname": "string",
  "first_name": "string",
  "middle_name": "string",
  "gender": "male",
  "marital_status": "single",
  "date_of_birth": "2024-11-15",
  "country_of_birth": "string",
  "nationality": "string",
  "uk_city_address": "string",
  "town": "string",
  "borough": "string",
  "address_line_one": "string",
  "address_line_two": "string",
  "post_code": "string",
  "state_of_origin": "string",
  "local_govt": "string",
  "ngn_address_line_one": "string",
  "ngn_address_line_two": "string",
  "ngn_state": "string",
  "town_of_origin": "string",
  "phone_number": "string",
  "height": "string",
}
```

Application for minors (people below 16 years) includes all other fields above in addition to the fields below 

```json
{
  "guardian_surname": "string",
  "guardian_firstname": "string",
  "guardian_nin": "string"
}
```

### Choices 
Fields that are restricted to specific values are listed below 

- **title**:  
  `miss, mrs, mr`

- **gender**:  
  `male, female, other`

- **marital_status**:  
  `single, married, divorced, widowed, separated`


### Required documents explained

```
To confirm your appointment, remember to bring one of the following proofs of ID:

1.Nigerian Passport: Expired or Current
2.For those without a Nigerian passport, bring the original birth certificate and Nigerian passport data page of either parent.

If you've booked for an infant, bring:
1.One (1) passport photograph with a grey background.
2.Parent or guardian must provide their NIN for all minors.
3.Ensure at least one parent/guardian accompanies the child during the appointment.
```


## Edit a Nigerian NIN

**Endpoint:** `/nin/update/{id}/`  
**Method:** `PATCH`  
**Permissions:** IsAuthenticated, IsAdmin

**Request body:**

```json
{
  "email_address": "user@example.com",
  "preferred_date_of_appointment": "2024-11-15",
  "appointment_time": "00:00",
  "bvn": "11111111111",
  "title": "miss",
  "surname": "string",
  "first_name": "string",
  "middle_name": "string",
  "gender": "male",
  "marital_status": "single",
  "date_of_birth": "2024-11-15",
  "country_of_birth": "string",
  "nationality": "string",
  "uk_city_address": "string",
  "town": "string",
  "borough": "string",
  "address_line_one": "string",
  "address_line_two": "string",
  "post_code": "string",
  "state_of_origin": "string",
  "local_govt": "string",
  "ngn_address_line_one": "string",
  "ngn_address_line_two": "string",
  "ngn_state": "string",
  "town_of_origin": "string",
  "phone_number": "string",
  "height": "string",
}
```


## Get details of an Nin
Ghana passport is divided into two For Adults and for minors

**Endpoint:** `/nin/detail/{id}/`  
**Method:** `GET`  
**Permissions:** IsAuthenticated, IsAdmin

**Sample response:** 

```json
{
  "status": "success",
  "data": {
    "id": "f1fbcdd0-c767-4486-8a9f-8fcdddc83806",
    "application": {
      "id": "160efd2e-ed11-4018-b390-ace38648106a",
      "created": "2024-11-22T15:30:56.118070Z",
      "updated": "2024-11-22T15:30:56.149343Z",
      "status": "pending",
      "has_paid": false,
      "application_type": "nin",
      "country_application": "nigeria",
      "tracking_id": "108722",
      "created_account": true,
      "completed_form": true,
      "completed_payment": false,
      "attended_appointment": false,
      "uploaded_biometric_slip": false,
      "received_document": false,
      "reference_id": "f1fbcdd0-c767-4486-8a9f-8fcdddc83806",
      "appointment_pack_tracking": null,
      "document_tracking": null,
      "user": "d413c189-923b-4843-862c-4eef0c0dba6b"
    },
    "email_address": "string",
    "preferred_date_of_appointment": "2024-11-15",
    "appointment_time": "00:00:00",
    "bvn": "string",
    "title": "miss",
    "surname": "string",
    "first_name": "string",
    "middle_name": "string",
    "gender": "male",
    "marital_status": "single",
    "date_of_birth": "2024-11-15",
    "country_of_birth": "2024-11-15",
    "nationality": "string",
    "uk_city_address": "string",
    "town": "string",
    "borough": "string",
    "address_line_one": "string",
    "address_line_two": "string",
    "post_code": "string",
    "state_of_origin": "string",
    "local_govt": "string",
    "ngn_address_line_one": "string",
    "ngn_address_line_two": "string",
    "ngn_state": "string",
    "town_of_origin": "string",
    "phone_number": "string",
    "height": "string",
    "guardian_surname": null,
    "guardian_firstname": null,
    "guardian_nin": null
  },
  "message": "",
  "success": true
}
```

