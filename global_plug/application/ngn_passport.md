## Apply for a Nigerian passport

**Endpoint:** `/passport/ngn/apply/`  
**Method:** `POST`  
**Permissions:** IsAuthenticated

**Request body:**

```json
{
  "next_of_kin": {
    "full_name": "Kirk Oyinye",
    "relationship": "Sister",
    "adress_line": "Back of jemmyland hotel",
    "state": "Abuja",
    "local_govt": "Nsukka",
    "city": "Mararaba",
    "postal_code": "901001",
    "telephone": "+2349039427166"
  },
  "nigerian_contact": {
    "state_of_origin": "Enugu",
    "home_town": "Nsukka",
    "address_line_one": "Somewhere close by",
    "local_govt": "Nsukka",
    "city": "Nsukka",
    "postal_code": "10010"
  },
  "uk_contact": {
    "phone_number": "049128168542",
    "address_one": "somewhere in the uk",
    "address_two": "somewhere also in the uk",
    "city": "boston",
    "country": "United Kindom",
    "postal_code": "890839"
  },
  "email": "udokyrian@gmail.com",
  "nin": "9992222",
  "type_of_application": "fresh_passport",
  "booklet_type": "32",
  "validity": 7,
  "passport_number": "8593032938300",
  "first_name": "Kyrian",
  "surname": "Onuh",
  "date_of_birth": "2024-09-02",
  "place_of_birth": "Behind",
  "marital_status": "single",
  "occupation": "Backend developer",
  "mother_maiden_name": "Acid",
  "title": "mr",
  "intl_passport_document": "<file>",
  "birth_certificate": "<file>",
  "data_page_or_death_cert": "<file>",
  "passport_photo": "<file>",
  "nigerian_passport_document": "<file>",
  "supporting_documents": [
    {
      "document": "<file>"
    }
  ],
}
```

### Choices 

Fields that are restricted to specific values are listed below 

### Request Body Explanation
Fields that are restricted to specific values are listed below:

- **type_of_application**:  
  `fresh_passport, renew_passport, lost_passport, damaged_passport, change of data`

- **booklet_type**:  
  `32, 64`

- **validity**:  
  `5, 10`

- **title**:  
  `miss, mrs, mr`

- **marital_status**:  
  `single, married, divorced, widowed, separated`



**Responses:**

**201 created:** Application created successfully

```json
{
  "id": "f4d2ebaf-42ff-4a20-8396-0d85a845968b",
  "application": {
    "id": "a2bf8bd3-e41e-4669-bd9f-7ce41e2cb334"
    //...other application details
  },
  "next_of_kin": {
    "id": 10
    //..other next of kin details
  },
  "nigerian_contact": {
    "id": 10,
    "state_of_origin": "Enugu"
    //..other nigerian contact details
  },
  "uk_contact": {
    "id": 12
    //.. other uk contact details
  },
  "email": "udokyrian@gmail.com",
  "nin": "9992222",
  "type_of_application": "fresh_passport",
  "booklet_type": "32",
  "validity": 7,
  "passport_number": "8593032938300",
  "title": "mr",
  "first_name": "Kyrian",
  "surname": "Onuh",
  "date_of_birth": "2024-09-02",
  "place_of_birth": "Behind",
  "marital_status": "single",
  "occupation": "Backend developer",
  "mother_maiden_name": "Acid",
  "intl_passport_document": null,
  "birth_certificate": null,
  "data_page_or_death_cert": null,
  "passport_photo": null,
  "nigerian_passport_document": null
}
```

**400 bad request:** Request body is malformed

```json
{
  "status": "failure",
  "data": null,
  "message": "email - This field is required.",//Reason why request failed
  "success": false
}
```
