# User Registration Endpoint

## POST /users/register

### Description
This endpoint is used to register a new user. It requires the user's first name, last name, email, and password.

### Request Body
The request body should be a JSON object containing the following fields:
- `fullname`: An object containing:
  - `firstname`: The user's first name (minimum 3 characters, required)
  - `lastname`: The user's last name (minimum 3 characters, optional)
- `email`: The user's email address (must be a valid email, required)
- `password`: The user's password (minimum 6 characters, required)

Example:
```json
{
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "john.doe@example.com",
  "password": "password123"
}
```

### Responses

#### Success
- **Status Code**: 201 Created
- **Response Body**: A JSON object containing the authentication token and user details.

Example:
```json
{
  "token": "your_jwt_token_here",
  "user": {
    "_id": "user_id_here",
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john.doe@example.com"
  }
}
```

#### Validation Errors
- **Status Code**: 400 Bad Request
- **Response Body**: A JSON object containing an array of validation error messages.

Example:
```json
{
  "errors": [
    {
      "msg": "Invalid Email",
      "param": "email",
      "location": "body"
    },
    {
      "msg": "First name must be atleast 3 characters",
      "param": "fullname.firstname",
      "location": "body"
    },
    {
      "msg": "Password must be atleast 6 characters",
      "param": "password",
      "location": "body"
    }
  ]
}
```

### Notes
- Ensure that the `Content-Type` header is set to `application/json` when making the request.
- The `password` field will be hashed before storing in the database.

# User Login Endpoint

## POST /users/login

### Description
This endpoint is used to log in an existing user. It requires the user's email and password.

### Request Body
The request body should be a JSON object containing the following fields:
- `email`: The user's email address (must be a valid email, required)
- `password`: The user's password (minimum 6 characters, required)

Example:
```json
{
  "email": "john.doe@example.com",
  "password": "password123"
}
```

### Responses

#### Success
- **Status Code**: 200 OK
- **Response Body**: A JSON object containing the authentication token and user details.

Example:
```json
{
  "token": "your_jwt_token_here",
  "user": {
    "_id": "user_id_here",
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john.doe@example.com"
  }
}
```

#### Validation Errors
- **Status Code**: 400 Bad Request
- **Response Body**: A JSON object containing an array of validation error messages.

Example:
```json
{
  "errors": [
    {
      "msg": "Invalid Email",
      "param": "email",
      "location": "body"
    },
    {
      "msg": "Password must be atleast 6 characters",
      "param": "password",
      "location": "body"
    }
  ]
}
```

#### Authentication Errors
- **Status Code**: 401 Unauthorized
- **Response Body**: A JSON object containing an error message.

Example:
```json
{
  "message": "Invalid email or password"
}
```

### Notes
- Ensure that the `Content-Type` header is set to `application/json` when making the request.

# User Profile Endpoint

## GET /users/profile

### Description
This endpoint is used to retrieve the profile of the currently authenticated user.

### Request Headers
- `Authorization`: Bearer token of the authenticated user (required)

### Responses

#### Success
- **Status Code**: 200 OK
- **Response Body**: A JSON object containing the user details.

Example:
```json
{
  "_id": "user_id_here",
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "john.doe@example.com"
}
```

#### Authentication Errors
- **Status Code**: 401 Unauthorized
- **Response Body**: A JSON object containing an error message.

Example:
```json
{
  "message": "Authentication required"
}
```

### Notes
- Ensure that the `Authorization` header is set to `Bearer <token>` when making the request.

# User Logout Endpoint

## GET /users/logout

### Description
This endpoint is used to log out the currently authenticated user.

### Request Headers
- `Authorization`: Bearer token of the authenticated user (required)

### Responses

#### Success
- **Status Code**: 200 OK
- **Response Body**: A JSON object containing a success message.

Example:
```json
{
  "message": "Logged out successfully"
}
```

#### Authentication Errors
- **Status Code**: 401 Unauthorized
- **Response Body**: A JSON object containing an error message.

Example:
```json
{
  "message": "Authentication required"
}
```

### Notes
- Ensure that the `Authorization` header is set to `Bearer <token>` when making the request.

# Captain Registration Endpoint

## POST /captains/register

### Description
This endpoint is used to register a new captain. It requires the captain's first name, last name, email, password, and vehicle details.

### Request Body
The request body should be a JSON object containing the following fields:
- `fullname`: An object containing:
  - `firstname`: The captain's first name (minimum 3 characters, required)
  - `lastname`: The captain's last name (minimum 3 characters, optional)
- `email`: The captain's email address (must be a valid email, required)
- `password`: The captain's password (minimum 6 characters, required)
- `vehicle`: An object containing:
  - `color`: The vehicle's color (minimum 3 characters, required)
  - `plate`: The vehicle's plate number (minimum 3 characters, required)
  - `capacity`: The vehicle's capacity (minimum 1, required)
  - `vehicleType`: The type of vehicle (must be one of 'car', 'motorcycle', 'auto', required)

Example:
```json
{
  "fullname": {
    "firstname": "Jane", // minimum 3 characters
    "lastname": "Doe" // optional, minimum 3 characters
  },
  "email": "jane.doe@example.com", // must be a valid email
  "password": "password123", // minimum 6 characters
  "vehicle": {
    "color": "Red", // minimum 3 characters
    "plate": "XYZ123", // minimum 3 characters
    "capacity": 4, // minimum 1
    "vehicleType": "car" // must be one of 'car', 'motorcycle', 'auto'
  }
}
```

### Responses

#### Success
- **Status Code**: 201 Created
- **Response Body**: A JSON object containing the captain details and authentication token.

Example:
```json
{
  "token": "your_jwt_token_here",
  "captain": {
    "_id": "captain_id_here",
    "fullname": {
      "firstname": "Jane",
      "lastname": "Doe"
    },
    "email": "jane.doe@example.com",
    "vehicle": {
      "color": "Red",
      "plate": "XYZ123",
      "capacity": 4,
      "vehicleType": "car"
    }
  }
}
```

#### Validation Errors
- **Status Code**: 400 Bad Request
- **Response Body**: A JSON object containing an array of validation error messages.

Example:
```json
{
  "errors": [
    {
      "msg": "Invalid Email",
      "param": "email",
      "location": "body"
    },
    {
      "msg": "Firstname must be atleast 3 characters",
      "param": "fullname.firstname",
      "location": "body"
    },
    {
      "msg": "Password must be atleast 6 characters",
      "param": "password",
      "location": "body"
    },
    {
      "msg": "Color must be atleast 3 characters long",
      "param": "vehicle.color",
      "location": "body"
    },
    {
      "msg": "Plate must be atleast 3 characters long",
      "param": "vehicle.plate",
      "location": "body"
    },
    {
      "msg": "Capacity must be atleast 1",
      "param": "vehicle.capacity",
      "location": "body"
    },
    {
      "msg": "Invalid vehicle type",
      "param": "vehicle.vehicleType",
      "location": "body"
    }
  ]
}
```

### Notes
- Ensure that the `Content-Type` header is set to `application/json` when making the request.

# Captain Login Endpoint

## POST /captains/login

### Description
This endpoint is used to log in an existing captain. It requires the captain's email and password.

### Request Body
The request body should be a JSON object containing the following fields:
- `email`: The captain's email address (must be a valid email, required)
- `password`: The captain's password (minimum 6 characters, required)

Example:
```json
{
  "email": "jane.doe@example.com", // must be a valid email
  "password": "password123" // minimum 6 characters
}
```

### Responses

#### Success
- **Status Code**: 200 OK
- **Response Body**: A JSON object containing the authentication token and captain details.

Example:
```json
{
  "token": "your_jwt_token_here",
  "captain": {
    "_id": "captain_id_here",
    "fullname": {
      "firstname": "Jane",
      "lastname": "Doe"
    },
    "email": "jane.doe@example.com",
    "vehicle": {
      "color": "Red",
      "plate": "XYZ123",
      "capacity": 4,
      "vehicleType": "car"
    }
  }
}
```

#### Validation Errors
- **Status Code**: 400 Bad Request
- **Response Body**: A JSON object containing an array of validation error messages.

Example:
```json
{
  "errors": [
    {
      "msg": "Invalid Email",
      "param": "email",
      "location": "body"
    },
    {
      "msg": "Password must be atleast 6 characters",
      "param": "password",
      "location": "body"
    }
  ]
}
```

#### Authentication Errors
- **Status Code**: 401 Unauthorized
- **Response Body**: A JSON object containing an error message.

Example:
```json
{
  "message": "Invalid email or password"
}
```

### Notes
- Ensure that the `Content-Type` header is set to `application/json` when making the request.

# Captain Profile Endpoint

## GET /captains/profile

### Description
This endpoint is used to retrieve the profile of the currently authenticated captain.

### Request Headers
- `Authorization`: Bearer token of the authenticated captain (required)

### Responses

#### Success
- **Status Code**: 200 OK
- **Response Body**: A JSON object containing the captain details.

Example:
```json
{
  "captain": {
    "_id": "captain_id_here",
    "fullname": {
      "firstname": "Jane",
      "lastname": "Doe"
    },
    "email": "jane.doe@example.com",
    "vehicle": {
      "color": "Red",
      "plate": "XYZ123",
      "capacity": 4,
      "vehicleType": "car"
    }
  }
}
```

#### Authentication Errors
- **Status Code**: 401 Unauthorized
- **Response Body**: A JSON object containing an error message.

Example:
```json
{
  "message": "Authentication required"
}
```

### Notes
- Ensure that the `Authorization` header is set to `Bearer <token>` when making the request.

# Captain Logout Endpoint

## GET /captains/logout

### Description
This endpoint is used to log out the currently authenticated captain.

### Request Headers
- `Authorization`: Bearer token of the authenticated captain (required)

### Responses

#### Success
- **Status Code**: 200 OK
- **Response Body**: A JSON object containing a success message.

Example:
```json
{
  "message": "Logged out successfully"
}
```

#### Authentication Errors
- **Status Code**: 401 Unauthorized
- **Response Body**: A JSON object containing an error message.

Example:
```json
{
  "message": "Authentication required"
}
```

### Notes
- Ensure that the `Authorization` header is set to `Bearer <token>` when making the request.



