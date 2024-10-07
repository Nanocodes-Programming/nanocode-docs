## 1. Add category

**Endpoint:** `/product/category/add/`  
**Method:** `POST`  
**Permissions:** IsAdmin  

**Description:** Adds a new category.

### Request Body:
```json
{
  "category_name": "string",
  "is_active": true
}
```

### Responses:
**201 Created:** Category added successfully.
```json
  "status": "success",
  "entity": {
    "category": {
      "id": 4,
      "category_name": "Waste basket",
      "date_created": "2024-06-28T08:49:09.892423Z",
      "is_active": true
    }
  },
  "message": "Category created",
  "success": true
}

```

**400 Bad request:** Category name already exists
```json
{
  "status": "failure",
  "entity": {},
  "message": "Category name already exists",
  "success": false
}
```


**403 Forbidden:** User permissions not qualified
```json
{
  "detail": "You do not have permission to perform this action."
}
```

---

## 2. List all categories

**Endpoint:** `/product/category/list/`  
**Method:** `GET`  
**Permissions:** IsAuthenticated, IsStaff  

**Description:** Retrieves all the categories available.


### Responses:
**200 OK:** Categories retrieved succsesfully.
```json
{
  "status": "success",
  "entity": [
    {
      "id": 1,
      "category_name": "Solar",
      "date_created": "2024-06-26T16:11:58.722802Z",
      "is_active": true
    },
    {
      "id": 2,
      "category_name": "Camera items",
      "date_created": "2024-06-27T00:33:18.945242Z",
      "is_active": true
    },
  ],
  "message": "",
  "success": true
}
```

**403 Forbidden:** User permissions not qualified
```json
{
  "detail": "You do not have permission to perform this action."
}
```


---

## 3. Add product

**Endpoint:** `/product/add/`  
**Method:** `POST`  
**Permissions:** isAuthenticated, isAdmin  

**Description:** Authenticates user credentials and returns an access token and a refresh token for subsequent requests.

### Request Body:
```json
{
  "name": "Solar",
  "description": "This solar is very big oo",
  "cost_price": "100000",
  "selling_price": "150000",
  "stock_quantity": 100,
  "is_available": true,
  "reorder_level": 10,
  "category": 1,
  "images":[],
  "warehouse": "e0938671-197e-4c36-bc52-d81864223c2c"
}
```
#### images: A list of image files
#### warehouse: the id of the warehouse in which this product is to be located

### Responses:
**201 CREATED:** Product created successfully
```json
{
    "status": "success",
    "entity": {
        "product": {
            "id": 21,
            "name": "A 6x6 solar pack",
            "description": "This is a solar",
            "cost_price": "60000.00",
            "selling_price": "65000.00",
            "stock_quantity": 10,
            "date_added": "2024-06-28T09:03:11.680100Z",
            "is_available": true,
            "reorder_level": 15,
            "category": 1,
            "warehouse": "e0938671-197e-4c36-bc52-d81864223c2c"
        },
        "images": [
            {
                "id": 9,
                "image": "/media/products/2024/03/28/pexels-canvastudio-3153198_1_1.webp",
                "image_name": "pexels-canvastudio-3153198 (1) (1).webp",
                "product": 21
            },
            {
                "id": 10,
                "image": "/media/products/2024/03/28/pexels-canvastudio-3153198_1.jpg",
                "image_name": "pexels-canvastudio-3153198 (1).jpg",
                "product": 21
            }
        ]
    },
    "message": "Product created successfully",
    "success": true
}
```

**400 Bad request:** Stock quantity below minimum
```json
{
    "status": "failure",
    "entity": {},
    "message": "Stock quantity must be greater than zero",
    "success": false
}
```

**403 Forbidden:** User permissions not qualified
```json
{
  "detail": "You do not have permission to perform this action."
}
```

---

## 4. List all products

**Endpoint:** `/product/list/`  
**Method:** `GET`  
**Permissions:** IsStaff  

**Description:** Retrieves all available products.

### Responses:
**200 OK:** Products retrieved successfully.
```json
{
  "status": "success",
  "entity": [
    {
      "id": 20,
      "category": {
        "id": 1,
        "category_name": "Solar",
        "date_created": "2024-06-26T16:11:58.722802Z",
        "is_active": true
      },
      "product_images": [
        {
          "id": 7,
          "image": "/media/products/2024/11/28/pexels-canvastudio-3153198_1_1.webp",
          "image_name": "pexels-canvastudio-3153198 (1) (1).webp",
          "product": 20
        },
        {
          "id": 8,
          "image": "/media/products/2024/11/28/pexels-canvastudio-3153198_1.jpg",
          "image_name": "pexels-canvastudio-3153198 (1).jpg",
          "product": 20
        }
      ],
      "name": "A 6x6 solar pack",
      "description": "This is a solar",
      "cost_price": "60000.00",
      "selling_price": "65000.00",
      "stock_quantity": 100,
      "date_added": "2024-06-28T02:11:21.422505Z",
      "is_available": true,
      "reorder_level": 15,
      "warehouse": "e0938671-197e-4c36-bc52-d81864223c2c"
    },
    {
      "id": 21,
      "category": {
        "id": 1,
        "category_name": "Solar",
        "date_created": "2024-06-26T16:11:58.722802Z",
        "is_active": true
      },
      "product_images": [
        {
          "id": 9,
          "image": "/media/products/2024/03/28/pexels-canvastudio-3153198_1_1.webp",
          "image_name": "pexels-canvastudio-3153198 (1) (1).webp",
          "product": 21
        },
        {
          "id": 10,
          "image": "/media/products/2024/03/28/pexels-canvastudio-3153198_1.jpg",
          "image_name": "pexels-canvastudio-3153198 (1).jpg",
          "product": 21
        }
      ],
      "name": "A 6x6 solar pack",
      "description": "This is a solar",
      "cost_price": "60000.00",
      "selling_price": "65000.00",
      "stock_quantity": 10,
      "date_added": "2024-06-28T09:03:11.680100Z",
      "is_available": true,
      "reorder_level": 15,
      "warehouse": "e0938671-197e-4c36-bc52-d81864223c2c"
    }
  ],
  "message": null,
  "success": true
}
```

**403 Forbidden:** User permissions not qualified
```json
{
  "detail": "You do not have permission to perform this action."
}
```
