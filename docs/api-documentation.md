# API Documentation Example

This document describes a sample REST API.

## Base URL

```
https://api.example.com
```

## Authentication

API requests require an authentication token.

Example header:

```
Authorization: Bearer <token>
```

## Endpoints

### Get Users

```
GET /users
```

Description:

Returns a list of registered users.

Example response:

```
{
  "users": [
    {
      "id": 1,
      "username": "alice"
    }
  ]
}
```

### Create User

```
POST /users
```

Request body:

```
{
  "username": "bob"
}
```

Response:

```
{
  "id": 2,
  "username": "bob"
}
```
