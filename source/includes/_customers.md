# Resources

A list of documented API resources is provided below.

# Customers

<b><u>Endpoint</u></b>

`/api/customers`

A Customer represents a "Patient". You can create a new customer, retrieve or modify an existing customer using its **Juvonno ID** or its **Chart Num**. 

Only **Juvonno ID** is treated as a unique identifier in our system. If you're querying using **Chart Num**, you must supply a unique existing number or else the program will throw corresponding error codes. 

<br>

<b><u>Endpoint Summary</u></b>

Method | Endpoint | Action
-------|----------|-------
<span class='http-post'>POST</span> | /api/<span class='pink'>customers</span> | create a <b>new customer</b>
<span class='http-get'>GET</span> | /api/<span class='pink'>customers</span>/**21**</span> | retrieve a <b>single</b> customer with ID <b>21</b>
<span class='http-get'>GET</span> | /api/<span class='pink'>customers</span>/<span class='blue'>chart</span>/**CHART1234**</span> | retrieve a <b>single</b> customer with Chart # <b>CHART1234</b>
<span class='http-put'>PUT</span> | /api/<span class='pink'>customers</span>/**21** | update a customer with ID <b>21</b>
<span class='http-put'>PUT</span> | /api/<span class='pink'>customers</span>/<span class='blue'>chart</span>/**CHART1234**</span> | update a <b>single</b> customer with Chart # <b>CHART1234</b>
<span class='http-delete'>DELETE</span> | /api/<span class='pink'>customers</span>/**21** | delete customer with ID <b>21</b>

## Create a new Customer

### HTTP Request

`POST https://tenant-id.juvonno.com/api/customers`

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
  "last_name": "Doe",
  "date_of_birth": "1989-12-01",
  "gender": "male"   
}
```

> Example Response:

```json
{
  "customer": {
    "id": 1,
    "num": {
      "chart": "CHART1234"     
    },
    "first_name": "John",
    "last_name": "Doe",
    "gender": "male",
    "date_of_birth": "1989-12-01",
    "status": "active"                 
  }
}
```

This endpoint creates a new customer.

### Query Parameters

Parameter | Description
--------- | ------- |
api_key | Always include your api_key in all of your requests.

### Request Body

- application/json
- application/x-www-form-urlencoded

<br>

Parameter | Required | Description
--------- | -------- | -----------
first_name | Y | Customer's first name
last_name | Y | Customer's last name
date_of_birth | Y | Customer's DOB
gender | Y | Must be one of "male", "female", "private" or "unknown"
chart_num | N | This can be used to match against your own customer's ID
preferred_language | N | Must be one of "english" or "french"
status | N | Must be one of "active", "inactive", "discharged" or "deleted"
branch_id | N | This refers to the Branch's Juvonno ID. See [Branch Resource](#branches) to learn more.<br>You can use either "branch_id", "branch_code" or "branch_name" 
branch_code | N | You can use either "branch_id", "branch_code" or "branch_name" 
branch_name | N | You can use either "branch_id", "branch_code" or "branch_name" 


## Retrieve a Customer using Juvonno ID

### HTTP Request

`GET https://tenant-id.juvonno.com/api/customers/{customerId}`

> Retrieve a customer who has a Juvonno ID of 21: 

```http
GET https://tenant-id.juvonno.com/api/customers/21?api_key={YOUR_API_KEY}
```

```shell 
cURL -X GET "https://tenant-id.juvonno.com/api/customers/21
?api_key={YOUR_API_KEY}"
```

> Example Response:

```json
{
  "customer": {
    "id": 21,
    "num": {
      "chart": "CHART1234"     
    },
    "first_name": "John",
    "last_name": "Doe",
    "gender": "male",
    "date_of_birth": "1989-12-01",
    "status": "active"                 
  }
}
```

### Query Parameters

Parameter | Description
--------- | ------- |
api_key | Always include your api_key in all of your requests.


### URL Parameters

Parameter | Description
--------- | -----------
customerID | The Juvonno ID of the customer to be retrieved


## Retrieve a Customer using Chart Num

### HTTP Request

`GET https://tenant-id.juvonno.com/api/customers/chart/{number}`

> Retrieve a customer who has a Chart Num of "CHART1234": 

```http
GET https://tenant-id.juvonno.com/api/customers/chart/CHART1234?api_key={YOUR_API_KEY}
```

```shell 
cURL -X GET "https://tenant-id.juvonno.com/api/customers/chart/CHART1234
?api_key={YOUR_API_KEY}"
```

> Example Response:

```json
{
  "customer": {
    "id": 21,
    "num": {
      "chart": "CHART1234"     
    },
    "first_name": "John",
    "last_name": "Doe",
    "gender": "male",
    "date_of_birth": "1989-12-01",
    "status": "active"                 
  }
}
```

### Query Parameters

Parameter | Description
--------- | ------- |
api_key | Always include your api_key in all of your requests.


### URL Parameters

Parameter | Description
--------- | -----------
number | The chart number of the customer to be retrieved

## Customer Custom Fields

The API supports a `custom_fields` array on customer write and read operations, so clients can set and retrieve customer custom field values using ID/value pairs.

### How It Works

- Each entry has the shape `{ custom_field_id, value }`
- `custom_field_id`: integer ID of an existing customer custom field definition
- `value`: string, nullable
- Partial merge behavior: only included custom field IDs are changed; omitted IDs remain as-is
- To clear a value, send `null` for the `value` of that `custom_field_id`

### Where To Use It

- `POST /customers` (create customer)
- `PUT /customers/{customerId}` (update customer)
- `PUT /customers/chart/{chartNumber}` (update customer by chart number)

Customer response objects also include `custom_fields` as current ID/value pairs.

### Example: Update One Custom Field, Clear Another

#### Request

```json
{
  "first_name": "Alex",
  "last_name": "Miller",
  "date_of_birth": "1990-05-10",
  "gender": "male",
  "custom_fields": [
    {
      "custom_field_id": 123,
      "value": "Prefers evening appointments"
    },
    {
      "custom_field_id": 456,
      "value": null
    }
  ]
}
```

#### Behavior

- Field `123` is set to `"Prefers evening appointments"`
- Field `456` is cleared
- Any other existing custom fields on that customer are unchanged

#### Typical Response Fragment

```json
{
  "id": 10025,
  "first_name": "Alex",
  "last_name": "Miller",
  "custom_fields": [
    { "custom_field_id": 123, "value": "Prefers evening appointments" },
    { "custom_field_id": 456, "value": null }
  ]
}
```

### Notes

- `custom_field_id` must refer to a valid existing customer custom field definition
- Use `null` only when you intentionally want to clear the stored value
- Omitted custom fields are preserved (not removed or reset)
