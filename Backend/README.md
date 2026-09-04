# Backend API Documentation

## Register User

Creates a new user account and returns an authentication token.

### Endpoint

```http
POST /users/register
```

If the backend is running locally on the default port:

```text
http://localhost:3000/users/register
```

### Request Headers

```http
Content-Type: application/json
```

### Request Body

The request body must be JSON with the following structure:

```json
{
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "john.doe@example.com",
  "password": "secret123"
}
```

#### Required Data

| Field | Type | Required | Requirements |
| --- | --- | --- | --- |
| `fullname.firstname` | String | Yes | At least 3 characters |
| `fullname.lastname` | String | No | Optional |
| `email` | String | Yes | Must be a valid email address |
| `password` | String | Yes | At least 6 characters |

### Successful Response

**Status:** `201 Created`

```json
{
  "user": {
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john.doe@example.com"
  },
  "token": "<jwt-token>"
}
```

The password is stored as a hash and is not included in the response.

### Validation Error

**Status:** `400 Bad Request`

Returned when one or more fields do not meet the validation requirements.

```json
{
  "errors": [
    {
      "type": "field",
      "value": "invalid-email",
      "msg": "Please enter a valid email address",
      "path": "email",
      "location": "body"
    }
  ]
}
```

### Status Codes

| Status Code | Description |
| --- | --- |
| `201 Created` | User registered successfully |
| `400 Bad Request` | Request data is missing or invalid |
| `500 Internal Server Error` | Unexpected server or database error |

### Example with cURL

```bash
curl -X POST http://localhost:3000/users/register \
  -H "Content-Type: application/json" \
  -d '{
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john.doe@example.com",
    "password": "secret123"
  }'
```
