## Apply for a Canadian visa

**Endpoint:** `/visa/canada/apply/`  
**Method:** `POST`  
**Permissions:** IsAuthenticated

**Request body:**

```json
{
  "first_name": 1,
  "middle_name": "King",
  "surname": "Kong",
  "uk_phone_number": "+412384928",
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
  "appointment_center": "london",

  "passport_first_last_pages": "<file>",
  "passport_stamps": "<file>",
  "employment_letters": "<file>",
  "original_brp": "<file>",
  "brp_copy": "<file>",
  "employment_confirmation_letter": "<file>",
  "hotel_booking_confirmation": "<file>",
  "payslips": "<file>",
  "bank_statements": "<file>"
}
```

## Request Body Explanation

Fields that are restricted to specific values are listed below:

_gender:_ `male, female, other`

_employment_status:_ `employed, student, self_employed, unemployed`

_marital_status:_ `single, married, divorced, widowed, separated`

_appointment_center:_ `london, manchester, endinburgh`

### Required documents explained:

```
We need your passport, BRP and University/Employment Details.

To facilitate a smooth online submission process for your visa application, please ensure you have the following documents ready for submission

- Passport first and last page in one PDF
- Passport pages with steal and stamps in one PDF
- Your original employment letters.
- Original BRP (Biometric Residence Permit) and copy
- Employment confirmation letter
- recent 3 months' payslips in one PDF
- Bank statements from the past 3 months in one PDF
- Hotel booking confirmation.
```

## Edit a Canadian visa

**Endpoint:** `/visa/canada/edit/{id}/`  
**Method:** `PATCH`  
**Permissions:** IsAuthenticated,

**Request body:**

```json
{
  "first_name": 1,
  "middle_name": "King",
  "surname": "Kong",
  "uk_phone_number": "+412384928",
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
  "appointment_center": "london",

  "passport_first_last_pages": "<file>",
  "passport_stamps": "<file>",
  "employment_letters": "<file>",
  "original_brp": "<file>",
  "brp_copy": "<file>",
  "employment_confirmation_letter": "<file>",
  "hotel_booking_confirmation": "<file>",
  "payslips": "<file>",
  "bank_statements": "<file>"
}
```


## Get the details of a canada visa


**Endpoint:** `/visa/canada/detail/{id}/`  
**Method:** `GET`  
**Permissions:** IsAuthenticated, isAdmin


**Sample response:**

```json
{
  "status": "success",
  "data": {
    "id": "ff34bc89-b488-4ad4-8989-000f8b562585",
    "application": {
      "id": "fd7bb545-7b89-413f-976b-3280e76c61cd",
      "created": "2024-11-19T19:54:35.945501Z",
      "updated": "2024-11-19T19:54:35.976804Z",
      "status": "pending",
      "has_paid": false,
      "application_type": "visa",
      "country_application": "usa",
      "tracking_id": "126133",
      "created_account": true,
      "completed_form": true,
      "completed_payment": false,
      "attended_appointment": false,
      "uploaded_biometric_slip": false,
      "received_document": false,
      "reference_id": "ff34bc89-b488-4ad4-8989-000f8b562585",
      "user": "d413c189-923b-4843-862c-4eef0c0dba6b"
    },
    "first_name": "1",
    "middle_name": "string",
    "surname": "string",
    "uk_phone_number": "string",
    "address_line_one": "string",
    "address_line_two": "string",
    "postal_code": "string",
    "city": "string",
    "gender": "male",
    "employment_status": "employed",
    "comp_uni_name": "string",
    "comp_uni_address_one": "string",
    "comp_uni_address_two": "string",
    "comp_uni_post_code": "string",
    "preferred_travelling_date": "2024-11-19",
    "brp_number": "string",
    "marital_status": "single",
    "appointment_center": "london",
    "passport_first_last_pages": null,
    "passport_stamps": null,
    "employment_letters": null,
    "original_brp": null,
    "brp_copy": null,
    "employment_confirmation_letter": null,
    "hotel_booking_confirmation": null,
    "payslips": null,
    "bank_statements": null
  },
  "message": "",
  "success": true
}
```
