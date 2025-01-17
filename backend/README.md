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

# Get Coordinates Endpoint

## GET /maps/get-coordinates

### Description
This endpoint is used to get the coordinates (latitude and longitude) of a given address.

### Request Query Parameters
- `address`: The address to get coordinates for (must be a string, minimum 3 characters, required)

Example:
```
GET /maps/get-coordinates?address=1600+Amphitheatre+Parkway,+Mountain+View,+CA
```

### Responses

#### Success
- **Status Code**: 200 OK
- **Response Body**: A JSON object containing the latitude and longitude of the address.

Example:
```json
{
  "ltd": 37.4224764,
  "lng": -122.0842499
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
      "msg": "Invalid value",
      "param": "address",
      "location": "query"
    }
  ]
}
```

#### Not Found
- **Status Code**: 404 Not Found
- **Response Body**: A JSON object containing an error message.

Example:
```json
{
  "message": "Coordinates not found"
}
```

### Notes
- Ensure that the `Authorization` header is set to `Bearer <token>` when making the request.

# Get Distance and Time Endpoint

## GET /maps/get-distance-time

### Description
This endpoint is used to get the distance and estimated travel time between two locations.

### Request Query Parameters
- `origin`: The starting location (must be a string, minimum 3 characters, required)
- `destination`: The destination location (must be a string, minimum 3 characters, required)

Example:
```
GET /maps/get-distance-time?origin=New+York,+NY&destination=Los+Angeles,+CA
```

### Responses

#### Success
- **Status Code**: 200 OK
- **Response Body**: A JSON object containing the distance and estimated travel time between the locations.

Example:
```json
{
  "distance": {
    "text": "2,789 mi",
    "value": 4488372
  },
  "duration": {
    "text": "1 day 18 hours",
    "value": 151200
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
      "msg": "Invalid value",
      "param": "origin",
      "location": "query"
    },
    {
      "msg": "Invalid value",
      "param": "destination",
      "location": "query"
    }
  ]
}
```

#### Internal Server Error
- **Status Code**: 500 Internal Server Error
- **Response Body**: A JSON object containing an error message.

Example:
```json
{
  "message": "Internal server error"
}
```

### Notes
- Ensure that the `Authorization` header is set to `Bearer <token>` when making the request.

# Get AutoComplete Suggestions Endpoint

## GET /maps/get-suggestions

### Description
This endpoint is used to get autocomplete suggestions for a given input.

### Request Query Parameters
- `input`: The input string to get suggestions for (must be a string, minimum 3 characters, required)

Example:
``GET /maps/get-suggestions?input=1600+Amphitheatre
```

### Responses

#### Success
- **Status Code**: 200 OK
- **Response Body**: A JSON array containing the autocomplete suggestions.

Example:
```json
[
  "1600 Amphitheatre Parkway, Mountain View, CA, USA",
  "1600 Amphitheatre Pkwy, Mountain View, CA 94043, USA"
]
```

#### Validation Errors
- **Status Code**: 400 Bad Request
- **Response Body**: A JSON object containing an array of validation error messages.

Example:
```json
{
  "errors": [
    {
      "msg": "Invalid value",
      "param": "input",
      "location": "query"
    }
  ]
}
```

#### Internal Server Error
- **Status Code**: 500 Internal Server Error
- **Response Body**: A JSON object containing an error message.

Example:
```json
{
  "message": "Internal server error"
}
```

### Notes
- Ensure that the `Authorization` header is set to `Bearer <token>` when making the request.

# Create Ride Endpoint

## POST /rides/create

### Description
This endpoint is used to create a new ride. It requires the user's pickup location, destination, and vehicle type.

### Request Body
The request body should be a JSON object containing the following fields:
- `pickup`: The pickup location (must be a string, minimum 3 characters, required)
- `destination`: The destination location (must be a string, minimum 3 characters, required)
- `vehicleType`: The type of vehicle (must be one of 'auto', 'car', 'moto', required)

Example:
```json
{
  "pickup": "1600 Amphitheatre Parkway, Mountain View, CA", // minimum 3 characters
  "destination": "1 Infinite Loop, Cupertino, CA", // minimum 3 characters
  "vehicleType": "car" // must be one of 'auto', 'car', 'moto'
}
```

### Responses

#### Success
- **Status Code**: 201 Created
- **Response Body**: A JSON object containing the ride details.

Example:
```json
{
  "_id": "ride_id_here",
  "user": "user_id_here",
  "pickup": "1600 Amphitheatre Parkway, Mountain View, CA",
  "destination": "1 Infinite Loop, Cupertino, CA",
  "otp": "123456",
  "fare": 50,
  "status": "pending"
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
      "msg": "Invalid pickup address",
      "param": "pickup",
      "location": "body"
    },
    {
      "msg": "Invalid destination address",
      "param": "destination",
      "location": "body"
    },
    {
      "msg": "Invalid vehicle type",
      "param": "vehicleType",
      "location": "body"
    }
  ]
}
```

### Notes
- Ensure that the `Content-Type` header is set to `application/json` when making the request.

# Get Fare Endpoint

## GET /rides/get-fare

### Description
This endpoint is used to get the fare estimate for a ride between two locations.

### Request Query Parameters
- `pickup`: The pickup location (must be a string, minimum 3 characters, required)
- `destination`: The destination location (must be a string, minimum 3 characters, required)

Example:
```
GET /rides/get-fare?pickup=1600+Amphitheatre+Parkway,+Mountain+View,+CA&destination=1+Infinite+Loop,+Cupertino,+CA
```

### Responses

#### Success
- **Status Code**: 200 OK
- **Response Body**: A JSON object containing the fare estimate for each vehicle type.

Example:
```json
{
  "auto": 30,
  "car": 50,
  "moto": 20
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
      "msg": "Invalid pickup address",
      "param": "pickup",
      "location": "query"
    },
    {
      "msg": "Invalid destination address",
      "param": "destination",
      "location": "query"
    }
  ]
}
```

### Notes
- Ensure that the `Authorization` header is set to `Bearer <token>` when making the request.

# Confirm Ride Endpoint

## POST /rides/confirm

### Description
This endpoint is used to confirm a ride by a captain. It requires the ride ID.

### Request Body
The request body should be a JSON object containing the following field:
- `rideId`: The ID of the ride to confirm (must be a valid MongoDB ObjectId, required)

Example:
```json
{
  "rideId": "ride_id_here" // must be a valid MongoDB ObjectId
}
```

### Responses

#### Success
- **Status Code**: 200 OK
- **Response Body**: A JSON object containing the confirmed ride details.

Example:
```json
{
  "_id": "ride_id_here",
  "user": {
    "_id": "user_id_here",
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john.doe@example.com"
  },
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
  },
  "pickup": "1600 Amphitheatre Parkway, Mountain View, CA",
  "destination": "1 Infinite Loop, Cupertino, CA",
  "otp": "123456",
  "fare": 50,
  "status": "accepted"
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
      "msg": "Invalid ride id",
      "param": "rideId",
      "location": "body"
    }
  ]
}
```

### Notes
- Ensure that the `Content-Type` header is set to `application/json` when making the request.

# Start Ride Endpoint

## GET /rides/start-ride

### Description
This endpoint is used to start a ride by a captain. It requires the ride ID and OTP.

### Request Query Parameters
- `rideId`: The ID of the ride to start (must be a valid MongoDB ObjectId, required)
- `otp`: The OTP for the ride (must be a string, exactly 6 characters, required)

Example:
```
GET /rides/start-ride?rideId=ride_id_here&otp=123456
```

### Responses

#### Success
- **Status Code**: 200 OK
- **Response Body**: A JSON object containing the started ride details.

Example:
```json
{
  "_id": "ride_id_here",
  "user": {
    "_id": "user_id_here",
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john.doe@example.com"
  },
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
  },
  "pickup": "1600 Amphitheatre Parkway, Mountain View, CA",
  "destination": "1 Infinite Loop, Cupertino, CA",
  "otp": "123456",
  "fare": 50,
  "status": "ongoing"
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
      "msg": "Invalid ride id",
      "param": "rideId",
      "location": "query"
    },
    {
      "msg": "Invalid OTP",
      "param": "otp",
      "location": "query"
    }
  ]
}
```

### Notes
- Ensure that the `Authorization` header is set to `Bearer <token>` when making the request.

# End Ride Endpoint

## POST /rides/end-ride

### Description
This endpoint is used to end a ride by a captain. It requires the ride ID.

### Request Body
The request body should be a JSON object containing the following field:
- `rideId`: The ID of the ride to end (must be a valid MongoDB ObjectId, required)

Example:
```json
{
  "rideId": "ride_id_here" // must be a valid MongoDB ObjectId
}
```

### Responses

#### Success
- **Status Code**: 200 OK
- **Response Body**: A JSON object containing the ended ride details.

Example:
```json
{
  "_id": "ride_id_here",
  "user": {
    "_id": "user_id_here",
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john.doe@example.com"
  },
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
  },
  "pickup": "1600 Amphitheatre Parkway, Mountain View, CA",
  "destination": "1 Infinite Loop, Cupertino, CA",
  "otp": "123456",
  "fare": 50,
  "status": "completed"
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
      "msg": "Invalid ride id",
      "param": "rideId",
      "location": "body"
    }
  ]
}
```

### Notes
- Ensure that the `Content-Type` header is set to `application/json` when making the request.



