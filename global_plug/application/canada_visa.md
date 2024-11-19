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

*appointment_center:* `london, manchester, endinburgh`

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