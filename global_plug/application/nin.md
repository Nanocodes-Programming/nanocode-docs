## Apply for a Nigerian passport

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
