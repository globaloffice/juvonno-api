# Branches

<b>Endpoint</b>

`/api/branches`

A Branch represents a "Clinic Location". You can create a new branch, retrieve or modify an existing branch using its **Juvonno ID**. 

## List all Branches

### HTTP Request

`GET https://tenant-id.juvonno.com/api/branches`

> List all Branches: 

```http
GET https://tenant-id.juvonno.com/api/branches?api_key={YOUR_API_KEY}
```

```shell 
cURL -X POST "https://tenant-id.juvonno.com/api/branches
?api_key={YOUR_API_KEY}"
```

> Example Response:

```json
{
  "list": [
    {
      "id": 1,
      "code": "ALBCLI",
      "name": "Alberta Clinic"
    },
    { 
      "id": 2,
      "code": "BRNCLI",
      "name": "Brandon Clinic"
    }   
  ]
}
```

This endpoint lists all branches in the system.

### Query Parameters

Parameter | Description
--------- | ------- |
api_key | Always include your api_key in all of your requests.
