## Apply for a Nigerian NIN

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
