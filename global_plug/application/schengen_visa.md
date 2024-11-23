## Apply for a Schengen visa

**Endpoint:** `/visa/schengen/apply/`  
**Method:** `POST`  
**Permissions:** IsAuthenticated

**Request body:**

```json
{
  "first_name": "Kyrian",
  "middle_name": "Udochukwu",
  "surname": "Onuh",
  "uk_phone_number": "+8143015512",
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

  "passport_document": "<file>",
  "brp_document": "<file>",
  "passport_photos": "<file>",
  "employment_confirmation_letter": "<file>",
  "bank_statements": "<file>",
  "hotel_booking_confirmation": "<file>",
  "flight_tickets": "<file>",
  "travel_insurance": "<file>",
  "payslips": "<file>"
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
- Passport
- BRP (Biometric Residence Permit)
- 2 recent passport photographs
- Employment confirmation letter and recent 3 months' payslips
- Bank statements from the past 3 months.
- Hotel booking confirmation. (we will get this)
- Flight tickets matching your hotel stay dates. (we will get this)
- Travel insurance covering the entirety of your trip across the Europe or Schengen area. (we could help get this)
```

## Edit a Schengen visa

**Endpoint:** `/visa/schengen/edit/{id}/`  
**Method:** `PATCH`  
**Permissions:** IsAuthenticated

**Request body:**

```json
{
  "first_name": "Kyrian",
  "middle_name": "Udochukwu",
  "surname": "Onuh",
  "uk_phone_number": "+8143015512",
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
  "passport_document": "<file>",
  "brp_document": "<file>",
  "passport_photos": "<file>",
  "employment_confirmation_letter": "<file>",
  "bank_statements": "<file>",
  "hotel_booking_confirmation": "<file>",
  "flight_tickets": "<file>",
  "travel_insurance": "<file>",
  "payslips": "<file>"
}
```

## Get the details of a schengen visa

**Endpoint:** `/visa/schengen/detail/{id}/`  
**Method:** `GET`  
**Permissions:** IsAuthenticated, IsAdmin

```json
{
  "status": "success",
  "data": {
    "id": "f8803306-ca9c-4c3b-abdc-8d631abb58f5",
    "application": {
      "id": "06513027-5fde-42b3-8b72-3d3edc84ebba",
      "created": "2024-09-09T14:53:14.288265Z",
      "updated": "2024-09-13T04:04:44.894048Z",
      "status": "pending",
      "has_paid": false,
      "application_type": "visa",
      "country_application": "nigeria",
      "tracking_id": "175696",
      "created_account": true,
      "completed_form": true,
      "completed_payment": false,
      "attended_appointment": false,
      "uploaded_biometric_slip": true,
      "received_document": false,
      "reference_id": null,
      "user": "452d7d4a-c54f-4592-b533-92dc9ec87ee5"
    },
    "first_name": "Kyrian",
    "middle_name": "Udochukwu",
    "surname": "Onuh",
    "uk_phone_number": "+8143015512",
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
    "passport_document": "http://localhost:8000/media/schengen/visa/passport_document/Onuh_Kyrian_Udochukwu_Resume_1.pdf",
    "brp_document": null,
    "passport_photos": null,
    "employment_confirmation_letter": null,
    "bank_statements": null,
    "hotel_booking_confirmation": null,
    "flight_tickets": null,
    "travel_insurance": null,
    "payslips": null
  },
  "message": "",
  "success": true
}
```
