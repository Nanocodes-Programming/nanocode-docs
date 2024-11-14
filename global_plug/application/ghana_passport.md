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

### Other applications
[Nigerian passport Application](./ngn_passport.md)





