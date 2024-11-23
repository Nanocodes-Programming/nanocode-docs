## Apply for a USA visa

**Endpoint:** `/visa/usa/apply/`  
**Method:** `POST`  
**Permissions:** IsAuthenticated

**Request body:**

```json
{
  "first_name": "Janefrances",
  "middle_name": "Onyinye",
  "surname": "Onuh",
  "uk_phone_number": "+41238492",
  "address_line_one": "Behind new york lamp",
  "address_line_two": "Opposite the first lamp",
  "postal_code": "100101",
  "city": "New york",
  "gender": "male",
  "employment_status": "employed",
  "comp_uni_name": "string",
  "comp_uni_address_one": "string",
  "comp_uni_address_two": "string",
  "comp_uni_post_code": "string",
  "preferred_travelling_date": "2024-09-03",
  "brp_number": "3315690873",
  "marital_status": "single",
  "original_passport_document": "<file>",
  "copy_passport_document": "<file>",
  "original_brp_document": "<file>",
  "copy_brp_document": "<file>",
  "user_photo": "<file>",
  "employment_confirmation_letter": "<file>",
  "bank_statements": "<file>",
  "hotel_booking_confirmation": "<file>"
}
```

## Request Body Explanation

Fields that are restricted to specific values are listed below:

_marital_status:_ `single, married, divorced, widowed, separated`

_gender:_ `male, female, other`

_employment_status:_ `employed, student, self_employed, unemployed`

_marital_status:_ `single, married, divorced, widowed, separated`

### Required documents explained:

```
The following documents will be needed, at the time of the Appointment: (Send this after full payment)
- Original Passport and copy
- Your Appointment confirmation (we will get this)
- Ds Confirmation Page (we will get this)
- Original BRP (Biometric Residence Permit) and copy
- One 5*5cm (2*2 inches) photo
- Employment confirmation letter and recent 3 months' payslips
- Bank statements from the past 3 months.
- Hotel booking confirmation. (we will get this)
```

## Edit a USA visa

**Endpoint:** `/visa/usa/edit/{id}/`  
**Method:** `PATCH`  
**Permissions:** IsAuthenticated, IsAdmin

**Request body:**

```json
{
  "first_name": "Janefrances",
  "middle_name": "Onyinye",
  "surname": "Onuh",
  "uk_phone_number": "+41238492",
  "address_line_one": "Behind new york lamp",
  "address_line_two": "Opposite the first lamp",
  "postal_code": "100101",
  "city": "New york",
  "gender": "male",
  "employment_status": "employed",
  "comp_uni_name": "string",
  "comp_uni_address_one": "string",
  "comp_uni_address_two": "string",
  "comp_uni_post_code": "string",
  "preferred_travelling_date": "2024-09-03",
  "brp_number": "3315690873",
  "marital_status": "single",
  "original_passport_document": "<file>",
  "copy_passport_document": "<file>",
  "original_brp_document": "<file>",
  "copy_brp_document": "<file>",
  "user_photo": "<file>",
  "employment_confirmation_letter": "<file>",
  "bank_statements": "<file>",
  "hotel_booking_confirmation": "<file>"
}
```

## Get the details of a usa visa

**Endpoint:** `/visa/usa/detail/{id}/`  
**Method:** `GET`  
**Permissions:** IsAuthenticated, IsAdmin


**Sample response:**

```json
{
  "status": "success",
  "data": {
    "id": "ec70ed5d-6b64-40dd-a2de-b73335b503c0",
    "application": {
      "id": "6b3afcdf-824d-44ac-b01e-80ce8020e51b",
      "created": "2024-11-22T15:03:21.691667Z",
      "updated": "2024-11-22T15:03:21.705787Z",
      "status": "pending",
      "has_paid": false,
      "application_type": "visa",
      "country_application": "usa",
      "tracking_id": "171719",
      "created_account": true,
      "completed_form": true,
      "completed_payment": false,
      "attended_appointment": false,
      "uploaded_biometric_slip": false,
      "received_document": false,
      "reference_id": "ec70ed5d-6b64-40dd-a2de-b73335b503c0",
      "user": "d413c189-923b-4843-862c-4eef0c0dba6b"
    },
    "first_name": "string",
    "middle_name": "string",
    "surname": "Onuh",
    "uk_phone_number": "+41238492",
    "address_line_one": "Behind new york lamp",
    "address_line_two": "Opposite the first lamp",
    "postal_code": "100101",
    "city": "New york",
    "gender": "male",
    "employment_status": "employed",
    "comp_uni_name": "string",
    "comp_uni_address_one": "string",
    "comp_uni_address_two": "string",
    "comp_uni_post_code": "string",
    "preferred_travelling_date": "2024-09-03",
    "brp_number": "3315690873",
    "marital_status": "single",
    "original_passport_document": null,
    "copy_passport_document": null,
    "original_brp_document": null,
    "copy_brp_document": null,
    "user_photo": null,
    "employment_confirmation_letter": null,
    "bank_statements": null,
    "hotel_booking_confirmation": null
  },
  "message": "",
  "success": true
}
```
