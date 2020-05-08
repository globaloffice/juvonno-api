# CRUD Operations

We follow standard RESTful CRUD operations. There will be a corresponding   
  `/api/ { RESOURCES - NAME }`   
collection of CRUD operations per Juvonno Object.
<aside class="notice">
CRUD stands for "Create", "Retrieve", "Update" and "Delete"
</aside>

## Create a new Resource

Always use **POST** to create a new resource.

`POST https://tenant-id.juvonno.com/api/{RESOURCES}/`

> Create a new Customer: 

```http
POST https://tenant-id.juvonno.com/api/customers?api_key={YOUR_API_KEY}
```

```shell 
cURL -X POST "https://tenant-id.juvonno.com/api/customers
?api_key={YOUR_API_KEY}"
```

> Example Request Body

```json
{
  "chart_num": "CHART1234",
  "first_name": "John",
  "last_name": "Doe"
}
```

### Query Parameters

Parameter | Description
--------- | ------- |
api_key | Always include your api_key in all of your requests.

### Request Body
- application/json
- application/x-www-form-urlencoded


## Retrieve an existing Resource

Always use **GET** to retrieve a resource.

`GET https://tenant-id.juvonno.com/api/{RESOURCES}/{RESOURCE_JUVONNO_ID}`

> Get a customer who has a Juvonno ID of 21: 

```http
GET https://tenant-id.juvonno.com/api/customers/21?api_key={YOUR_API_KEY}
```

```shell 
cURL -X GET "https://tenant-id.juvonno.com/api/customers/21
?api_key={YOUR_API_KEY}"
```

### Query Parameters

Parameter | Description
--------- | ------- |
api_key | Always include your api_key in all of your requests.


## Update an existing Resource

Always use **PUT** to update an existing resource.

`PUT https://tenant-id.juvonno.com/api/{RESOURCES}/{RESOURCE_JUVONNO_ID}`

> Update a customer who has a Juvonno ID of 21 with new phone number: 

```http
PUT https://tenant-id.juvonno.com/api/customers/21?api_key={YOUR_API_KEY}
```

```shell 
cURL -X PUT "https://tenant-id.juvonno.com/api/customers/21
?api_key={YOUR_API_KEY}"
```

> Request Body

```json
{
  "phone": "1-431-123-1234"
}
```

### Query Parameters

Parameter | Description
--------- | ------- |
api_key | Always include your api_key in all of your requests.

### Request Body
- application/json
- application/x-www-form-urlencoded


## Delete an existing Resource

Always use **DELETE** to delete a resource.

`DELETE https://tenant-id.juvonno.com/api/{RESOURCES}/{RESOURCE_JUVONNO_ID}`

> Delete a customer who has a Juvonno ID of 21: 

```http
DELETE https://tenant-id.juvonno.com/api/customers/21?api_key={YOUR_API_KEY}
```

```shell 
cURL -X DELETE "https://tenant-id.juvonno.com/api/customers/21
?api_key={YOUR_API_KEY}"
```

### Query Parameters

Parameter | Description
--------- | ------- |
api_key | Always include your api_key in all of your requests.

## Flexible Parameters

Sometimes an object can be accessed using different identifiers, Juvonno API provides the users with the flexibility of using other identifiers besides our main **"Juvonno ID"** to perform operations on the resource.

**Example Scenario:**

You want to create a new Staff and assign your staff to a clinic location called "Brandon Clinic".

A Clinic is represented by a "Branch Resource" in our API. A Branch can be identified by either its:

- Branch's Juvonno ID
- Branch's code
- Branch's name

In the request body, you can supply either parameter "branch_id", "branch_code" or "branch_name". Juvonno will try to map the branch to the staff based on the parameter your provided. Only one parameter needs to be supplied, although you can supply as many as you wish.

In case you have supplied more than one parameter (for example “branch_id” and “branch_name”), and if Juvonno has found a match with the first parameter, it will ignore and won’t map the second parameter provided. Mapping priority is in this exact order:  

`Branch_id  > Branch_code > Branch_name`

If your application has two branches with the same name “Brandon Clinic”, Juvonno API will return an Error with a detailed message asking you to supply a unique "branch_name" or use "branch_id" (Juvonno ID) instead. 

If your application has no branches with the name “Brandon Clinic”, Juvonno API will return an Error telling you that it was unable to find any record with such name. 
