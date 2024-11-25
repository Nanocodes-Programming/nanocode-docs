# Ghana passport flow documentation

## Apply for a Ghana passport 
Ghana passport is divided into two For Adults and for minors

**Endpoint:** `/passport/ghana/apply/`  
**Method:** `POST`  
**Permissions:** IsAuthenticated  

### Adult 

**Request body:**
```json
{
  "email": "user@example.com",
  "title": "miss",
  "surname": "string",
  "firstname": "string",
  "middle_name": "string",
  "maiden_name": "string",
  "profession": "string",
  "place_of_birth": "string",
  "date_of_birth": "2024-11-13",
  "marital_status": "single",
  "country_of_residence": "string",
  "height": 0,
  "color_of_eyes": "string",
  "color_of_hair": "string",
  "gender": "male",
  "address_line_one": "string",
  "address_line_two": "string",
  "town": "string",
  "borough": "string",
  "uk_city_address": "string",
  "post_code": "string",
  "phone_number": "string",
  "fathers_fullname": "string",
  "fathers_nationality": "string",
  "fathers_address": "string",
  "fathers_phone_number": "string",
  "mothers_fullname": "string",
  "mothers_nationality": "string",
  "mothers_address": "string",
  "mothers_phone_number": "string",
  "grand_parents_full_name": "string",
  "grand_parents_nationality": "string",
  "grand_parents_address": "string",
  "grand_parents_phone_number": "string",
  "previous_passport_issuing_office": "string",
  "previous_passport_number": "string",
  "guarantors_fullname": "string",
  "guarantors_address": "string",
  "guarantors_postcode": "string",
  "guarantors_email": "user@example.com",
  "declaration_by_applicant": "string",
  "ghana_citizenship_proof": "<file>",
  "parents_passport": "<file>",
  "passport_photo": "<file>",
  "ghanian_birth_certificate": "<file>",
  "school_certificate": "<file>",
  "drivers_license": "<file>",
  "identity_card": "<file>",
  "british_passport": "<file>"
}
```

Application for minors includes all other fields above in addition to the fields below 

```json
  "guardian_fullname": "string",
  "guardian_address": "string",
  "guardian_postcode": "string",
  "guardian_phone_number": "string",
  "guardian_signature": "string",
  "guardian_date_sign": "string"
```

### Choices 
Fields that are restricted to specific values are listed below 

_title:_ `miss, mrs, mr`

_gender:_ `male, female, other`

_marital_status:_ `single, married, divorced, widowed, separated`

### Documents 
Documents to be uploaded for ghana passport 

```json
{
  "ghana_citizenship_proof": "<file>",
  "parents_passport": "<file>",
  "passport_photo": "<file>",
  "ghanian_birth_certificate": "<file>",
  "school_certificate": "<file>",
  "drivers_license": "<file>",
  "identity_card": "<file>",
  "british_passport": "<file>"
}
```

From the above documents, the following are required 
`ghana_citizenship_proof, parents_passport, passport_photo`
while the rest are supporting documents and are optional

## Edit a Ghana passport
Ghana passport is divided into two For Adults and for minors

**Endpoint:** `/passport/ghana/update/{id}/`  
**Method:** `PATCH`  
**Permissions:** IsAuthenticated, IsAdmin

**Request body:**
```json
{
  "email": "user@example.com",
  "title": "miss",
  "surname": "string",
  "firstname": "string",
  "middle_name": "string",
  "maiden_name": "string",
  "profession": "string",
  "place_of_birth": "string",
  "date_of_birth": "2024-11-13",
  "marital_status": "single",
  "country_of_residence": "string",
  "height": 0,
  "color_of_eyes": "string",
  "color_of_hair": "string",
  "gender": "male",
  "address_line_one": "string",
  "address_line_two": "string",
  "town": "string",
  "borough": "string",
  "uk_city_address": "string",
  "post_code": "string",
  "phone_number": "string",
  "fathers_fullname": "string",
  "fathers_nationality": "string",
  "fathers_address": "string",
  "fathers_phone_number": "string",
  "mothers_fullname": "string",
  "mothers_nationality": "string",
  "mothers_address": "string",
  "mothers_phone_number": "string",
  "grand_parents_full_name": "string",
  "grand_parents_nationality": "string",
  "grand_parents_address": "string",
  "grand_parents_phone_number": "string",
  "previous_passport_issuing_office": "string",
  "previous_passport_number": "string",
  "guarantors_fullname": "string",
  "guarantors_address": "string",
  "guarantors_postcode": "string",
  "guarantors_email": "user@example.com",
  "declaration_by_applicant": "string",
  "ghana_citizenship_proof": "<file>",
  "parents_passport": "<file>",
  "passport_photo": "<file>",
  "ghanian_birth_certificate": "<file>",
  "school_certificate": "<file>",
  "drivers_license": "<file>",
  "identity_card": "<file>",
  "british_passport": "<file>",
  "guardian_fullname": "string",
  "guardian_address": "string",
  "guardian_postcode": "string",
  "guardian_phone_number": "string",
  "guardian_signature": "string",
  "guardian_date_sign": "string"
}
```


## Get details of a Ghana passport
Ghana passport is divided into two For Adults and for minors

**Endpoint:** `/passport/ghana/detail/{id}/`  
**Method:** `GET`  
**Permissions:** IsAuthenticated, IsAdmin

**Sample response:** 

```json
{
  "status": "success",
  "data": {
    "id": "9addba52-2cb2-441b-9544-eae617a02feb",
    "application": {
      "id": "cd74aae7-c1d0-4ce1-b4f0-3a3108eaa9f4",
      "created": "2024-11-13T09:41:41.799605Z",
      "updated": "2024-11-13T09:41:41.834811Z",
      "status": "pending",
      "has_paid": false,
      "application_type": "passport",
      "country_application": "ghana",
      "tracking_id": "152221",
      "created_account": true,
      "completed_form": true,
      "completed_payment": false,
      "attended_appointment": false,
      "uploaded_biometric_slip": false,
      "received_document": false,
      "reference_id": "9addba52-2cb2-441b-9544-eae617a02feb",
      "user": "d413c189-923b-4843-862c-4eef0c0dba6b"
    },
    "email": "someonebig@gmail.com",
    "title": "miss",
    "surname": "string",
    "firstname": "Kyrian devoloee",
    "middle_name": "string",
    "maiden_name": "string",
    "profession": "string",
    "place_of_birth": "string",
    "date_of_birth": "2024-11-13",
    "marital_status": "single",
    "country_of_residence": "string",
    "height": 0,
    "color_of_eyes": "string",
    "color_of_hair": "string",
    "gender": "male",
    "address_line_one": "string",
    "address_line_two": "string",
    "town": "string",
    "borough": "string",
    "uk_city_address": "string",
    "post_code": "string",
    "phone_number": "string",
    "fathers_fullname": "string",
    "fathers_nationality": "string",
    "fathers_address": "string",
    "fathers_phone_number": "string",
    "mothers_fullname": "string",
    "mothers_nationality": "string",
    "mothers_address": "string",
    "mothers_phone_number": "string",
    "grand_parents_full_name": "string",
    "grand_parents_nationality": "string",
    "grand_parents_address": "string",
    "grand_parents_phone_number": "string",
    "previous_passport_issuing_office": "string",
    "previous_passport_number": "string",
    "guarantors_fullname": "string",
    "guarantors_address": "string",
    "guarantors_postcode": "string",
    "guarantors_email": "user@example.com",
    "declaration_by_applicant": "string",
    "type_of_application": "attached",
    "guardian_fullname": "string",
    "guardian_address": "string",
    "guardian_postcode": "string",
    "guardian_phone_number": "string",
    "guardian_signature": "string",
    "guardian_date_sign": "string",
    "ghana_citizenship_proof": null,
    "parents_passport": null,
    "passport_photo": null,
    "ghanian_birth_certificate": null,
    "school_certificate": null,
    "drivers_license": null,
    "identity_card": null,
    "british_passport": null
  },
  "message": "",
  "success": true
}

```

### Other applications
[Nigerian passport Application](./ngn_passport.md)






