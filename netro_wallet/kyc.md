# kyc flow documentation

## NIN verification 
User has to provide their nin number and a selfie of themselves, the request is successful if the face in the selfie matches the face on the NIN 

Note: The selfie should be taken in the mobile app, user should not have an option of choosing an image from their gallery 

**Endpoint:** `/kyc/nin/`  
**Method:** `POST`  
**Permissions:** IsAuthenticated  

### Request body:
```json
{
  "nin_number": "11111111111",
  "image": "<file>"
}
```

### Responses:
**400 bad request:**

```json
{
    "status": "failure",
    "entity": {
        "match": false
    },
    "message": "The selfie does not match the image associated with the provided BVN, please try again",
    "success": false
}
```

**200 OK:**

```json
{
    "status": "success",
    "entity": {
        "match": true
    },
    "message": "NIN validation successful",
    "success": false
}
```


## BVN verification 
User has to provide their BVN number and a selfie of themselves, the request is successful if the face in the selfie matches the face on the BVN 

Note: The selfie should be taken in the mobile app, user should not have an option of choosing an image from their gallery 

**Endpoint:** `/kyc/bvn/`  
**Method:** `POST`  
**Permissions:** IsAuthenticated  

### Request body:
```json
{
  "bvn_number": "11111111111",
  "image": "<file>"
}
```

### Responses:
**400 bad request:**

```json
{
    "status": "failure",
    "entity": {
        "match": false
    },
    "message": "The selfie does not match the image associated with the provided BVN, please try again.",
    "success": false
}
```

**200 OK:**

```json
{
    "status": "success",
    "entity": {
        "match": true
    },
    "message": "BVN validation successful",
    "success": false
}
```