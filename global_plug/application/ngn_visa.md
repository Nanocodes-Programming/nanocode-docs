## Apply for a Nigerian visa

**Endpoint:** `/visa/ngn/apply/`  
**Method:** `POST`  
**Permissions:** IsAuthenticated

**Request body:**

```json
{
  "uk_contact": {
    "phone_number": "08143015512",
    "address_one": "Back of jemmyland",
    "address_two": "Back of the pole",
    "city": "ozeba way",
    "country": "United kingdom",
    "postal_code": "900902"
  },
  "ngn_contact": {
    "type_of_contact": "family",
    "inviting_full_name": "Bola",
    "contact_name": "Kweku the traveller",
    "phone_number": "09128168542",
    "contact_address": "His address",
    "city": "mararaba",
    "state": "abuja",
    "postal_code": "989009",
    "sponsor": "self"
  },
  "nationality": "Nigerian",
  "passport_type": "standard",
  "visa_type": "single_entry",
  "title": "miss",
  "surname": "onuh",
  "first_name": "kyrian",
  "middle_name": "onuh",
  "place_of_birth": "nsukka",
  "date_of_birth": "2024-09-04",
  "gender": "male",
  "marital_status": "single",
  "email_address": "user@example.com",
  "phone_number": "91248493029",
  "passport_number": "9493849339",
  "passport_expiry_date": "2024-09-04",
  "previous_nationality": "pluto",
  "occupation": "programmer",
  "arrival_date": "2024-09-04",
  "depature_date": "2024-09-04",
  "has_applied_for_nigerian_visa": "yes",
  "visa_application_location": "string",
  "visa_granted_or_rejected": "granted",
  "reason_visa_granted": "duh",
  "fingerprint_collected_prev": "yes",
  "has_served_in_military": "yes"
}
```

## Request Body Explanation

Fields that are restricted to specific values are listed below:

_passport_type_: `standard, diplomatic, official, un`

_visa_type_: `single_entry, multiple_entry, temp_work_permit, subject_to_regularisation`

_title_: `miss, mrs, mr`

_gender_; `male, female, other`

_marital_status:_ `single, married, divorced, widowed, separated`

_has_applied_for_nigerian_visa:_ `yes, no`
_visa_granted_or_rejected:_ `yes, no`

_fingerprint_collected_prev:_ `yes, no`

_has_served_in_military:_ `yes, no`

## Edit a Nigerian visa

**Endpoint:** `/visa/ngn/edit/{id}/`  
**Method:** `PATCH`  
**Permissions:** IsAuthenticated, IsAdmin

```json
{
  "uk_contact": {
    "phone_number": "08143015512",
    "address_one": "Back of jemmyland",
    "address_two": "Back of the pole",
    "city": "ozeba way",
    "country": "United kingdom",
    "postal_code": "900902"
  },
  "ngn_contact": {
    "type_of_contact": "family",
    "inviting_full_name": "Bola",
    "contact_name": "Kweku the traveller",
    "phone_number": "09128168542",
    "contact_address": "His address",
    "city": "mararaba",
    "state": "abuja",
    "postal_code": "989009",
    "sponsor": "self"
  },
  "nationality": "Nigerian",
  "passport_type": "standard",
  "visa_type": "single_entry",
  "title": "miss",
  "surname": "onuh",
  "first_name": "kyrian",
  "middle_name": "onuh",
  "place_of_birth": "nsukka",
  "date_of_birth": "2024-09-04",
  "gender": "male",
  "marital_status": "single",
  "email_address": "user@example.com",
  "phone_number": "91248493029",
  "passport_number": "9493849339",
  "passport_expiry_date": "2024-09-04",
  "previous_nationality": "pluto",
  "occupation": "programmer",
  "arrival_date": "2024-09-04",
  "depature_date": "2024-09-04",
  "has_applied_for_nigerian_visa": "yes",
  "visa_application_location": "string",
  "visa_granted_or_rejected": "granted",
  "reason_visa_granted": "duh",
  "fingerprint_collected_prev": "yes",
  "has_served_in_military": "yes"
}
```

## Get the details of a Nigerian Visa

**Endpoint:** `/visa/ngn/detail/{id}/`  
**Method:** `GET`  
**Permissions:** IsAuthenticated, IsAdmin

**Sample response:**

```json
{
  "status": "success",
  "data": {
    "id": "ca171e85-5d1d-4424-b152-c68a6ad04498",
    "uk_contact": {
      "id": 13,
      "phone_number": "08143015512",
      "address_one": "Back of jemmyland",
      "address_two": "Back of the pole",
      "city": "ozeba way",
      "country": "United kingdom",
      "postal_code": "900902"
    },
    "ngn_contact": {
      "id": 3,
      "type_of_contact": "family",
      "inviting_full_name": "Bola",
      "contact_name": "Kweku the traveller",
      "phone_number": "09128168542",
      "contact_address": "His address",
      "city": "mararaba",
      "state": "abuja",
      "postal_code": "989009",
      "sponsor": "self"
    },
    "application": {
      "id": "c8235941-048f-4372-92a9-4dd0be93a193",
      "created": "2024-11-22T16:03:43.095654Z",
      "updated": "2024-11-22T16:03:43.146778Z",
      "status": "pending",
      "has_paid": false,
      "application_type": "visa",
      "country_application": "nigeria",
      "tracking_id": "163961",
      "created_account": true,
      "completed_form": true,
      "completed_payment": false,
      "attended_appointment": false,
      "uploaded_biometric_slip": false,
      "received_document": false,
      "reference_id": "ca171e85-5d1d-4424-b152-c68a6ad04498",
      "user": "d413c189-923b-4843-862c-4eef0c0dba6b"
    },
    "nationality": "Nigerian",
    "passport_type": "standard",
    "visa_type": "single_entry",
    "title": "miss",
    "surname": "onuh",
    "first_name": "kyrian",
    "middle_name": "onuh",
    "place_of_birth": "nsukka",
    "date_of_birth": "2024-09-04",
    "gender": "male",
    "marital_status": "single",
    "email_address": "user@example.com",
    "phone_number": "91248493029",
    "passport_number": "9493849339",
    "passport_expiry_date": "2024-09-04",
    "previous_nationality": "pluto",
    "occupation": "programmer",
    "arrival_date": "2024-09-04",
    "depature_date": "2024-09-04",
    "has_applied_for_nigerian_visa": "yes",
    "visa_application_location": "string",
    "visa_granted_or_rejected": "granted",
    "reason_visa_granted": "duh",
    "fingerprint_collected_prev": "yes",
    "has_served_in_military": "yes"
  },
  "message": "",
  "success": true
}
```
