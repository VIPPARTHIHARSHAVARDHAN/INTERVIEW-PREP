# Backend and REST API Basics

> Placement-focused notes covering the **main backend and REST API concepts** commonly required for fresher software/backend interviews.
>
> Focus on understanding the concepts and being able to explain them with simple examples.

---

# 1. Backend Basics

## 1. What is Backend Development?

**Answer:**

Backend development is the development of the server-side part of an application.

The backend is responsible for:

- Processing requests
- Applying business logic
- Working with databases
- Authentication and authorization
- Returning responses to the frontend
- Integrating with external services

Example:

```text
Frontend
   ↓
HTTP Request
   ↓
Backend Server
   ↓
Business Logic
   ↓
Database
   ↓
Backend Response
   ↓
Frontend
```

---

## 2. Frontend vs Backend

**Answer:**

| Frontend | Backend |
|---|---|
| Runs mainly on the client/browser | Runs on the server |
| User interface | Business logic |
| HTML, CSS, JavaScript | Python, Java, Node.js, etc. |
| Sends requests | Processes requests |
| Displays results | Gets/stores/processes data |

Example:

```text
User clicks "Login"
        ↓
Frontend sends username/password
        ↓
Backend validates credentials
        ↓
Database is checked
        ↓
Backend sends response
        ↓
Frontend displays result
```

---

## 3. What is a Server?

**Answer:**

A server is a system that receives requests from clients, processes them, and sends responses.

Example:

```text
Client
  ↓ Request
Server
  ↓ Response
Client
```

A backend application commonly runs on a server and handles client requests.

---

## 4. What is a Client?

**Answer:**

A client is a system or application that sends requests to a server.

Examples:

```text
Web Browser
Mobile App
Frontend Application
Postman
```

---

## 5. What is a Client-Server Architecture?

**Answer:**

Client-server architecture separates an application into clients that request services and servers that process those requests.

```text
Client
  ↓
Server
  ↓
Database
```

The client communicates with the backend server, and the backend communicates with databases or other services.

---

## 6. What is Business Logic?

**Answer:**

Business logic contains the rules that determine how an application should behave.

Example:

```text
If account balance >= withdrawal amount
    → Allow withdrawal
Else
    → Reject withdrawal
```

The database stores the data, while business logic determines what should happen to that data.

---

## 7. What is an API?

**Answer:**

API stands for **Application Programming Interface**.

An API provides a way for different software components to communicate with each other.

Example:

```text
Frontend
   ↓
API Request
   ↓
Backend
   ↓
Database
```

The frontend does not need to directly access the database. It communicates with the backend through APIs.

---

## 8. Why do we need APIs?

**Answer:**

APIs allow different applications or components to communicate without needing to know each other's internal implementation.

For example:

```text
Mobile App
    ↓
REST API
    ↓
Backend
    ↓
Database
```

The mobile application can request data through the API without directly accessing the database.

---

# 2. HTTP Basics

## 9. What is HTTP?

**Answer:**

HTTP stands for **HyperText Transfer Protocol**.

It is a protocol used for communication between clients and servers.

Example:

```text
Client
  ↓ HTTP Request
Server
  ↓ HTTP Response
Client
```

REST APIs commonly use HTTP.

---

## 10. What is HTTPS?

**Answer:**

HTTPS stands for **HyperText Transfer Protocol Secure**.

It uses encryption through TLS to protect communication between the client and server.

```text
HTTP
→ Communication without TLS encryption

HTTPS
→ HTTP + TLS security
```

HTTPS helps protect sensitive information such as passwords and authentication tokens while they are transmitted.

---

## 11. HTTP vs HTTPS

**Answer:**

| HTTP | HTTPS |
|---|---|
| Not protected by TLS | Protected using TLS |
| Less secure for sensitive communication | More secure |
| Uses `http://` | Uses `https://` |

Production applications should generally use HTTPS.

---

## 12. What is an HTTP Request?

**Answer:**

An HTTP request is a message sent by a client to a server.

It can contain:

```text
HTTP Method
URL
Headers
Query Parameters
Request Body
```

Example:

```http
GET /users/101
```

---

## 13. What is an HTTP Response?

**Answer:**

An HTTP response is the message sent by the server back to the client.

It commonly contains:

```text
Status Code
Headers
Response Body
```

Example:

```http
HTTP/1.1 200 OK

{
    "id": 101,
    "name": "Ravi"
}
```

---

## 14. What are HTTP Headers?

**Answer:**

HTTP headers contain additional information about a request or response.

Examples:

```text
Content-Type
Authorization
Accept
User-Agent
```

Example:

```http
Authorization: Bearer <token>
Content-Type: application/json
```

---

## 15. What is Content-Type?

**Answer:**

`Content-Type` tells the server or client what type of data is being sent.

Example:

```http
Content-Type: application/json
```

This indicates that the request or response body contains JSON data.

---

# 3. HTTP Methods

## 16. What are the main HTTP methods?

**Answer:**

The main methods used in REST APIs are:

```text
GET
POST
PUT
PATCH
DELETE
```

They represent different operations on resources.

---

## 17. What is GET?

**Answer:**

GET is generally used to retrieve data from a server.

Example:

```http
GET /users
```

Response:

```json
[
    {
        "id": 1,
        "name": "Ravi"
    }
]
```

---

## 18. What is POST?

**Answer:**

POST is generally used to create a new resource or submit data to the server.

Example:

```http
POST /users
```

Request body:

```json
{
    "name": "Ravi",
    "age": 22
}
```

---

## 19. What is PUT?

**Answer:**

PUT is generally used to replace or completely update a resource.

Example:

```http
PUT /users/101
```

Request:

```json
{
    "name": "Ravi",
    "age": 23
}
```

---

## 20. What is PATCH?

**Answer:**

PATCH is generally used for a partial update of a resource.

Example:

```http
PATCH /users/101
```

Request:

```json
{
    "age": 23
}
```

Only the specified field needs to be changed.

---

## 21. What is DELETE?

**Answer:**

DELETE is used to delete a resource.

Example:

```http
DELETE /users/101
```

---

## 22. PUT vs PATCH

**Answer:**

| PUT | PATCH |
|---|---|
| Usually replaces the resource | Partially updates the resource |
| Complete representation is commonly sent | Only changed fields can be sent |
| Used for full update | Used for partial update |

Example:

```text
PUT
→ Update complete user

PATCH
→ Update only user's email
```

---

## 23. GET vs POST

**Answer:**

| GET | POST |
|---|---|
| Retrieves data | Usually creates/submits data |
| Parameters commonly in URL/query | Data commonly in request body |
| Generally safe/read-only | Can change server state |
| Should not modify resource state | May create or modify state |

---

# 4. REST API

## 24. What is REST?

**Answer:**

REST stands for **Representational State Transfer**.

REST is an architectural style for designing web APIs using standard HTTP concepts.

REST APIs commonly use:

```text
Resources
HTTP methods
HTTP status codes
JSON
Stateless communication
```

---

## 25. What is a REST API?

**Answer:**

A REST API is an API designed around REST principles and commonly uses HTTP methods to operate on resources.

Example:

```text
GET    /users
GET    /users/101
POST   /users
PUT    /users/101
PATCH  /users/101
DELETE /users/101
```

---

## 26. What is a Resource in REST?

**Answer:**

A resource represents an entity or object that an API exposes.

Examples:

```text
/users
/products
/orders
/employees
```

A specific resource can be identified using an ID.

```text
/users/101
/products/500
/orders/9001
```

---

## 27. What is a REST endpoint?

**Answer:**

An endpoint is a specific API URL through which a client can access a resource or operation.

Example:

```text
GET /users/101
```

Here:

```text
/users/101
→ Endpoint path

GET
→ HTTP method
```

---

## 28. What makes an API RESTful?

**Answer:**

Important REST principles include:

```text
Client-Server separation
Statelessness
Resource-based URLs
Uniform interface
Proper HTTP methods
Proper HTTP status codes
Cacheability where appropriate
```

For placement interviews, **statelessness and resource-based design** are especially important.

---

## 29. What does stateless mean in REST?

**Answer:**

Stateless means each request should contain the information necessary for the server to process it.

The server does not rely on stored session state from previous requests to understand the current request.

Example:

```text
Request 1
→ Contains authentication information

Request 2
→ Also contains required authentication information
```

Each request is independently understandable.

---

## 30. Why is statelessness useful?

**Answer:**

Stateless APIs are easier to scale because requests can be handled by different server instances without requiring a specific server to remember the client's previous request.

```text
Client
   ↓
Load Balancer
  ↙   ↓   ↘
Server1 Server2 Server3
```

---

## 31. What is a stateless API example?

**Answer:**

A client sends an authentication token with every request.

```http
GET /profile

Authorization: Bearer <token>
```

The server can validate the token without depending on a session stored on a specific server.

---

# 5. JSON

## 32. What is JSON?

**Answer:**

JSON stands for **JavaScript Object Notation**.

It is a lightweight data format commonly used for exchanging data between clients and APIs.

Example:

```json
{
    "id": 101,
    "name": "Ravi",
    "age": 22
}
```

---

## 33. Why is JSON commonly used in REST APIs?

**Answer:**

JSON is:

- Lightweight
- Human-readable
- Easy to parse
- Supported by many programming languages
- Convenient for representing structured data

---

## 34. JSON Object vs JSON Array

**Answer:**

A JSON object uses key-value pairs.

```json
{
    "id": 101,
    "name": "Ravi"
}
```

A JSON array contains multiple values or objects.

```json
[
    {
        "id": 101,
        "name": "Ravi"
    },
    {
        "id": 102,
        "name": "Arun"
    }
]
```

---

# 6. HTTP Status Codes

## 35. What are HTTP status codes?

**Answer:**

HTTP status codes indicate the result of an HTTP request.

They are grouped into:

```text
1xx → Informational
2xx → Success
3xx → Redirection
4xx → Client Error
5xx → Server Error
```

---

## 36. What is 200 OK?

**Answer:**

`200 OK` means the request was successfully processed.

Example:

```http
GET /users/101
→ 200 OK
```

---

## 37. What is 201 Created?

**Answer:**

`201 Created` indicates that a new resource was successfully created.

Example:

```http
POST /users
→ 201 Created
```

---

## 38. What is 204 No Content?

**Answer:**

`204 No Content` means the request was successfully processed but there is no response body to return.

It can be used for operations such as a successful deletion.

---

## 39. What is 400 Bad Request?

**Answer:**

`400 Bad Request` indicates that the server could not process the request because the request itself was invalid.

Examples:

```text
Invalid JSON
Missing required input
Invalid request format
```

---

## 40. What is 401 Unauthorized?

**Answer:**

`401 Unauthorized` generally means the request lacks valid authentication credentials.

Example:

```text
Missing token
Invalid token
Expired authentication credentials
```

---

## 41. What is 403 Forbidden?

**Answer:**

`403 Forbidden` means the server understood the request but the client does not have permission to perform the requested action.

Example:

```text
Authenticated user
        ↓
Attempts admin-only operation
        ↓
403 Forbidden
```

---

## 42. 401 vs 403

**Answer:**

```text
401
→ Authentication is missing or invalid.

403
→ Authentication may exist, but access is not allowed.
```

Simple example:

```text
401 → "Who are you?"

403 → "I know who you are, but you cannot do this."
```

---

## 43. What is 404 Not Found?

**Answer:**

`404 Not Found` means the requested resource could not be found.

Example:

```http
GET /users/999999
```

If that user does not exist:

```http
404 Not Found
```

---

## 44. What is 405 Method Not Allowed?

**Answer:**

`405 Method Not Allowed` means the HTTP method is not supported for the requested resource.

Example:

```text
Endpoint:
GET /users

Client:
DELETE /users
```

If DELETE is not supported for that endpoint, the server can return `405`.

---

## 45. What is 409 Conflict?

**Answer:**

`409 Conflict` indicates that the request conflicts with the current state of the resource.

Example:

```text
Trying to create a user with an ID
that already exists
```

The API may return:

```http
409 Conflict
```

---

## 46. What is 500 Internal Server Error?

**Answer:**

`500 Internal Server Error` indicates that an unexpected error occurred on the server.

Example:

```text
Application exception
Unexpected server failure
```

---

## 47. What is 503 Service Unavailable?

**Answer:**

`503 Service Unavailable` indicates that the server is temporarily unable to handle the request.

Possible reasons include:

```text
Server overload
Maintenance
Temporary service failure
```

---

## 48. Important status codes to remember

| Status | Meaning |
|---|---|
| 200 | OK |
| 201 | Created |
| 204 | No Content |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 405 | Method Not Allowed |
| 409 | Conflict |
| 500 | Internal Server Error |
| 503 | Service Unavailable |

---

# 7. URL, Path and Query Parameters

## 49. What is a Path Parameter?

**Answer:**

A path parameter is a value included directly in the URL path to identify a specific resource.

Example:

```text
GET /users/101
```

Here:

```text
101
→ Path parameter
```

---

## 50. What is a Query Parameter?

**Answer:**

A query parameter is used to provide additional information or filters in the URL.

Example:

```text
GET /users?city=Hyderabad
```

Here:

```text
city=Hyderabad
→ Query parameter
```

---

## 51. Path Parameter vs Query Parameter

**Answer:**

```text
Path Parameter
→ Usually identifies a specific resource

/users/101

Query Parameter
→ Usually filters, searches, sorts, or modifies retrieval behavior

/users?city=Hyderabad
```

---

## 52. What is pagination?

**Answer:**

Pagination divides a large result set into smaller pages.

Example:

```http
GET /users?page=1&limit=20
```

Instead of returning thousands of records at once, the API returns a smaller number of records.

---

## 53. Why is pagination important?

**Answer:**

Pagination helps:

- Reduce response size
- Reduce memory usage
- Improve response time
- Reduce network traffic
- Prevent unnecessarily large queries

---

## 54. What is filtering?

**Answer:**

Filtering returns only records matching specified conditions.

Example:

```http
GET /products?category=mobile
```

This requests products belonging to the mobile category.

---

## 55. What is sorting in an API?

**Answer:**

Sorting allows clients to request data in a particular order.

Example:

```http
GET /products?sort=price
```

The exact API syntax depends on the API design.

---

# 8. Authentication and Authorization

## 56. What is Authentication?

**Answer:**

Authentication verifies **who the user is**.

Example:

```text
Username + Password
        ↓
Authentication
        ↓
User identified
```

---

## 57. What is Authorization?

**Answer:**

Authorization determines **what an authenticated user is allowed to do**.

Example:

```text
User logged in
       ↓
Is user an Admin?
       ↓
Yes → Allow admin operation
No  → Deny access
```

---

## 58. Authentication vs Authorization

**Answer:**

```text
Authentication
→ Who are you?

Authorization
→ What are you allowed to do?
```

---

## 59. What is a token?

**Answer:**

A token is a credential that can be used to represent or authenticate a client/user after authentication.

Example:

```http
Authorization: Bearer <token>
```

The server validates the token before allowing access to protected resources.

---

## 60. What is JWT?

**Answer:**

JWT stands for **JSON Web Token**.

It is a compact token format commonly used for authentication and authorization.

A JWT typically contains:

```text
Header
Payload
Signature
```

---

## 61. What is the basic JWT authentication flow?

**Answer:**

```text
User Login
    ↓
Backend validates credentials
    ↓
JWT generated
    ↓
Client stores token
    ↓
Client sends token with requests
    ↓
Backend validates token
    ↓
Access granted/rejected
```

Example:

```http
Authorization: Bearer <JWT>
```

---

## 62. What is Bearer Authentication?

**Answer:**

Bearer authentication uses a token sent in the HTTP `Authorization` header.

Example:

```http
Authorization: Bearer <token>
```

The server validates the token and determines whether the request should be allowed.

---

## 63. Where should passwords be stored?

**Answer:**

Passwords should **never be stored as plain text**.

They should be stored using a strong password hashing algorithm with an appropriate salt.

Example concept:

```text
Password
   ↓
Password Hashing
   ↓
Stored Hash
```

---

# 9. REST API Design

## 64. How should REST API URLs be designed?

**Answer:**

URLs should generally represent resources using nouns rather than actions.

Good:

```text
GET /users
GET /users/101
GET /products
POST /orders
```

Avoid unnecessarily action-based URLs such as:

```text
/getUsers
/createUser
/deleteUser
```

The HTTP method already expresses the operation.

---

## 65. What is a good REST API endpoint for getting a user?

**Answer:**

```http
GET /users/101
```

Here:

```text
GET
→ Retrieve

/users
→ User resource

101
→ Specific user
```

---

## 66. What endpoint would you use to create a user?

**Answer:**

```http
POST /users
```

The user data is generally sent in the request body.

---

## 67. What endpoint would you use to update a user?

**Answer:**

For a complete update:

```http
PUT /users/101
```

For a partial update:

```http
PATCH /users/101
```

---

## 68. What endpoint would you use to delete a user?

**Answer:**

```http
DELETE /users/101
```

---

## 69. What is API versioning?

**Answer:**

API versioning allows an API to evolve without unexpectedly breaking existing clients.

Example:

```text
/api/v1/users
/api/v2/users
```

Different versions can support different API contracts.

---

## 70. Why is API versioning important?

**Answer:**

APIs are often used by multiple clients.

If the backend changes an existing API in a breaking way, older applications may stop working.

Versioning allows older clients to continue using the previous API contract while newer clients use the newer version.

---

# 10. Request and Response Example

## 71. Explain a complete REST API request.

**Answer:**

Example:

```http
POST /users
Content-Type: application/json

{
    "name": "Ravi",
    "age": 22
}
```

The server receives the request, validates the input, applies business logic, stores the data, and returns a response.

Example response:

```http
201 Created
Content-Type: application/json

{
    "id": 101,
    "name": "Ravi",
    "age": 22
}
```

---

## 72. What is request body?

**Answer:**

The request body contains data sent from the client to the server.

It is commonly used with methods such as:

```text
POST
PUT
PATCH
```

Example:

```json
{
    "name": "Ravi",
    "age": 22
}
```

---

## 73. What is response body?

**Answer:**

The response body contains the data returned by the server.

Example:

```json
{
    "id": 101,
    "name": "Ravi"
}
```

---

# 11. API Error Handling

## 74. Why is error handling important in APIs?

**Answer:**

Good error handling allows clients to understand why a request failed.

For example:

```json
{
    "error": "User not found"
}
```

combined with:

```http
404 Not Found
```

gives the client both a standard status code and useful information.

---

## 75. How should an API handle invalid input?

**Answer:**

The backend should validate the request and return an appropriate client-error status.

For example:

```text
Invalid input
    ↓
400 Bad Request
```

The response can provide a clear error message.

---

## 76. Should APIs expose internal error details?

**Answer:**

No.

Production APIs should avoid exposing sensitive internal information such as:

```text
Database passwords
Internal stack traces
Secret keys
Internal infrastructure details
```

The client should receive a safe error message while detailed information can be logged securely on the server.

---

# 12. CORS

## 77. What is CORS?

**Answer:**

CORS stands for **Cross-Origin Resource Sharing**.

It is a browser security mechanism that controls whether a web page from one origin can make requests to a different origin.

Example:

```text
Frontend:
https://frontend.example

Backend:
https://api.example
```

These are different origins, so the server needs to allow the required cross-origin requests.

---

## 78. Why does CORS occur?

**Answer:**

Browsers enforce the same-origin policy for security.

When frontend JavaScript tries to communicate with a different origin, the browser applies CORS rules to determine whether the request is allowed.

---

## 79. Is CORS a backend authentication mechanism?

**Answer:**

No.

CORS is primarily a browser security mechanism controlling cross-origin requests.

Authentication and authorization are separate concepts.

---

# 13. API Tools and Testing

## 80. What is Postman?

**Answer:**

Postman is a tool commonly used to test and interact with APIs.

It allows developers to send:

```text
GET
POST
PUT
PATCH
DELETE
```

requests and inspect responses.

---

## 81. How do you test a REST API?

**Answer:**

I would test:

```text
HTTP method
URL
Request headers
Request body
Status code
Response body
Authentication
Error cases
```

Example:

```text
POST /users
        ↓
Send JSON body
        ↓
Check status code
        ↓
Check response
```

---

## 82. What is API testing?

**Answer:**

API testing verifies that an API behaves correctly for valid and invalid requests.

It can test:

```text
Correct responses
Status codes
Validation
Authentication
Authorization
Error handling
Data correctness
```

---

# 14. Backend Architecture Basics

## 83. What is a three-tier architecture?

**Answer:**

Three-tier architecture separates an application into:

```text
Presentation Layer
       ↓
Business Logic Layer
       ↓
Data Layer
```

Example:

```text
Frontend
   ↓
Backend / Business Logic
   ↓
Database
```

---

## 84. What is the Controller-Service-Repository pattern?

**Answer:**

It separates backend responsibilities into different layers.

```text
Controller
   ↓
Service
   ↓
Repository
   ↓
Database
```

### Controller

Handles HTTP requests and responses.

### Service

Contains business logic.

### Repository

Handles data access.

This separation makes code easier to maintain and test.

---

## 85. Why separate business logic from the controller?

**Answer:**

Keeping business logic separate makes the application:

- Easier to test
- Easier to maintain
- Easier to reuse
- Less tightly coupled

Example:

```text
Controller
→ Receives request

Service
→ Applies business rules

Repository
→ Accesses database
```

---

# 15. API Security Basics

## 86. What are common API security practices?

**Answer:**

Important practices include:

```text
Use HTTPS
Validate input
Use authentication
Implement authorization
Protect credentials
Use secure password hashing
Avoid exposing sensitive errors
Apply rate limiting
Validate tokens
```

---

## 87. What is rate limiting?

**Answer:**

Rate limiting restricts how many requests a client can make within a certain period.

Example:

```text
100 requests / minute
```

If the client exceeds the limit, the server can reject additional requests temporarily.

---

## 88. Why is rate limiting important?

**Answer:**

Rate limiting can help:

- Prevent abuse
- Reduce excessive traffic
- Protect backend resources
- Mitigate some automated attacks
- Maintain service availability

---

## 89. What is input validation?

**Answer:**

Input validation checks whether data received from the client satisfies expected rules.

Example:

```text
Age must be an integer
Email must have valid format
Price must not be negative
Required fields must be present
```

Input validation should happen on the backend even if the frontend also validates the data.

---

# 16. Important Interview Scenarios

## 90. A client sends an invalid user ID. What response would you return?

**Answer:**

If the ID is syntactically valid but the user does not exist, I would typically return:

```http
404 Not Found
```

with an appropriate error response.

---

## 91. A client sends invalid JSON. What would you return?

**Answer:**

I would generally return:

```http
400 Bad Request
```

because the request format is invalid.

---

## 92. A user is logged in but tries to access an admin endpoint. What should happen?

**Answer:**

If the user is authenticated but does not have the required permission, the API should generally return:

```http
403 Forbidden
```

---

## 93. A request has no valid authentication token. What should happen?

**Answer:**

The API should generally return:

```http
401 Unauthorized
```

because the request does not contain valid authentication credentials.

---

## 94. The server encounters an unexpected exception. What should happen?

**Answer:**

The API can return:

```http
500 Internal Server Error
```

The detailed exception should be logged securely on the server rather than exposed to the client.

---

## 95. How would you design a user CRUD API?

**Answer:**

A basic design could be:

```text
GET    /users
GET    /users/{id}
POST   /users
PUT    /users/{id}
PATCH  /users/{id}
DELETE /users/{id}
```

These endpoints correspond to common CRUD operations.

---

## 96. What is CRUD?

**Answer:**

CRUD stands for:

```text
C → Create
R → Read
U → Update
D → Delete
```

REST API mapping:

```text
POST   → Create
GET    → Read
PUT/PATCH → Update
DELETE → Delete
```

---

# 17. ⭐ Top Placement Questions

## 97. What is Backend Development?

**Answer:**

Backend development deals with the server-side logic of an application, including APIs, business logic, database interaction, authentication, and processing client requests.

---

## 98. What is an API?

**Answer:**

An API provides a way for different software components to communicate with each other.

---

## 99. What is REST API?

**Answer:**

A REST API is an API designed around REST principles and commonly uses HTTP methods to work with resources.

---

## 100. What are HTTP methods?

**Answer:**

The main methods are:

```text
GET
POST
PUT
PATCH
DELETE
```

They are commonly used for retrieving, creating, updating, partially updating, and deleting resources.

---

## 101. GET vs POST?

**Answer:**

GET is generally used to retrieve data, while POST is generally used to submit data or create a resource.

---

## 102. PUT vs PATCH?

**Answer:**

PUT is generally used for complete replacement/update of a resource, while PATCH is generally used for partial updates.

---

## 103. What is a status code?

**Answer:**

A status code tells the client the result of an HTTP request.

Important examples:

```text
200 → Success
201 → Created
400 → Bad Request
401 → Authentication problem
403 → Permission denied
404 → Resource not found
500 → Server error
```

---

## 104. 401 vs 403?

**Answer:**

```text
401
→ Missing/invalid authentication

403
→ Authenticated but not allowed to access the resource
```

---

## 105. What is JSON?

**Answer:**

JSON is a lightweight data format commonly used to exchange structured data between clients and servers.

---

## 106. What is a REST resource?

**Answer:**

A resource represents an entity exposed through an API.

Examples:

```text
/users
/products
/orders
```

---

## 107. What is a REST endpoint?

**Answer:**

An endpoint is a specific API URL through which a client accesses a resource or performs an operation.

Example:

```http
GET /users/101
```

---

## 108. What is statelessness?

**Answer:**

Statelessness means each request contains the information needed for the server to process it, without relying on stored state from previous requests.

---

## 109. Authentication vs Authorization?

**Answer:**

```text
Authentication
→ Who are you?

Authorization
→ What are you allowed to do?
```

---

## 110. What is JWT?

**Answer:**

JWT is a compact token format commonly used to carry authentication information between a client and server.

---

## 111. What is CORS?

**Answer:**

CORS is a browser security mechanism that controls whether requests from one origin can access resources on another origin.

---

## 112. What is pagination?

**Answer:**

Pagination divides a large result set into smaller pages to reduce response size and improve API performance.

---

## 113. What is API versioning?

**Answer:**

API versioning allows an API to evolve while maintaining compatibility with existing clients.

Example:

```text
/api/v1/users
/api/v2/users
```

---

## 114. What is rate limiting?

**Answer:**

Rate limiting controls how many requests a client can make within a specific period to protect the API from excessive traffic or abuse.

---

# 18. ⭐ Most Important Scenario Questions

## 115. Design a basic User REST API.

**Answer:**

I would expose the user resource using standard REST endpoints:

```text
GET    /users
GET    /users/{id}
POST   /users
PUT    /users/{id}
PATCH  /users/{id}
DELETE /users/{id}
```

The controller would handle HTTP requests, the service layer would contain business logic, and the repository layer would communicate with the database.

---

## 116. How would you handle authentication in a REST API?

**Answer:**

A common approach is:

```text
User Login
   ↓
Validate Credentials
   ↓
Generate Token
   ↓
Client Sends Token
   ↓
Backend Validates Token
   ↓
Allow/Deny Request
```

HTTPS should be used to protect credentials and tokens during transmission.

---

## 117. How would you secure an API?

**Answer:**

I would use:

```text
HTTPS
Authentication
Authorization
Input validation
Secure password hashing
Token validation
Rate limiting
Safe error handling
```

I would also avoid exposing secrets and sensitive internal details.

---

## 118. How would you handle an API that is returning too much data?

**Answer:**

I would consider:

```text
Pagination
Filtering
Field selection
Compression where appropriate
```

The goal is to return only the data the client actually needs.

---

## 119. How would you improve a slow API?

**Answer:**

I would first identify the bottleneck instead of making assumptions.

I would investigate:

```text
Database queries
Indexes
Network latency
External API calls
Large response payloads
Application processing
Caching opportunities
```

Then optimize the actual bottleneck.

---

## 120. How would you handle an API failure?

**Answer:**

I would:

```text
1. Check the status code.
2. Check backend logs.
3. Identify the failing component.
4. Determine whether the issue is temporary.
5. Fix the root cause.
6. Retry only when appropriate.
7. Return a suitable error response.
```

---

# 19. Quick Revision Sheet

```text
BACKEND
│
├── Client
├── Server
├── Business Logic
├── Database
└── API
│
├── HTTP
│   ├── Request
│   ├── Response
│   ├── Headers
│   ├── Body
│   └── Status Codes
│
├── HTTP METHODS
│   ├── GET
│   ├── POST
│   ├── PUT
│   ├── PATCH
│   └── DELETE
│
├── REST
│   ├── Resources
│   ├── Endpoints
│   ├── Statelessness
│   ├── HTTP Methods
│   └── Status Codes
│
├── DATA
│   ├── JSON
│   ├── Request Body
│   ├── Response Body
│   ├── Path Parameters
│   ├── Query Parameters
│   └── Pagination
│
├── SECURITY
│   ├── Authentication
│   ├── Authorization
│   ├── JWT
│   ├── HTTPS
│   ├── CORS
│   ├── Input Validation
│   └── Rate Limiting
│
└── ARCHITECTURE
    ├── Controller
    ├── Service
    ├── Repository
    └── Database
```

---

# 20. Final Interview Priority

## ⭐⭐⭐⭐⭐ Must Know

```text
What is Backend Development?
What is an API?
What is REST?
What is REST API?
HTTP vs HTTPS
HTTP Request / Response
GET
POST
PUT
PATCH
DELETE
PUT vs PATCH
HTTP Status Codes
200
201
400
401
403
404
500
JSON
REST Resources
REST Endpoints
Statelessness
Path Parameters
Query Parameters
CRUD
Authentication
Authorization
Authentication vs Authorization
JWT
CORS
Pagination
API Security
API Versioning
```

## ⭐⭐⭐⭐ Know If Time Allows

```text
Controller-Service-Repository
Rate Limiting
API Testing
Postman
Error Handling
Caching
Three-Tier Architecture
```

---

# 21. Final Interview Strategy

For a fresher backend interview, be able to explain each major concept in this format:

```text
Definition
    ↓
Simple Explanation
    ↓
Example
    ↓
Real-world Usage
```

Example:

### Question: What is REST API?

**Answer:**

> "A REST API is an API designed using REST principles to allow clients and servers to communicate over HTTP. It represents data as resources and commonly uses methods such as GET, POST, PUT, PATCH, and DELETE. For example, `GET /users/101` can be used to retrieve a specific user. REST APIs are commonly used to connect frontend applications with backend services."

### Question: What is the difference between authentication and authorization?

**Answer:**

> "Authentication verifies who the user is, while authorization determines what that authenticated user is allowed to access. For example, logging in with a username and password is authentication, while checking whether that user has permission to access an admin endpoint is authorization."

### Question: What happens when you call a REST API?

**Answer:**

> "The client sends an HTTP request to the API endpoint. The backend receives the request, validates it, executes the required business logic, interacts with the database or other services if necessary, and then sends an HTTP response containing a status code and usually a response body."

---

# 22. Final Checklist

```text
☐ Explain frontend vs backend
☐ Explain client-server architecture
☐ Explain API
☐ Explain HTTP
☐ Explain HTTPS
☐ Explain request and response
☐ Explain HTTP headers
☐ Know GET
☐ Know POST
☐ Know PUT
☐ Know PATCH
☐ Know DELETE
☐ Know PUT vs PATCH
☐ Explain REST
☐ Explain REST API
☐ Explain resources
☐ Explain endpoints
☐ Explain statelessness
☐ Know JSON
☐ Know status codes
☐ Know 200
☐ Know 201
☐ Know 400
☐ Know 401
☐ Know 403
☐ Know 404
☐ Know 500
☐ Explain path parameters
☐ Explain query parameters
☐ Explain pagination
☐ Explain CRUD
☐ Explain authentication
☐ Explain authorization
☐ Explain JWT
☐ Explain CORS
☐ Explain rate limiting
☐ Explain API versioning
☐ Explain input validation
☐ Explain API security
☐ Explain Controller-Service-Repository
☐ Design a basic CRUD API
☐ Explain how you would secure an API
☐ Explain how you would troubleshoot a slow API
```

> **Placement focus:** Prioritize HTTP, REST, API endpoints, HTTP methods, status codes, JSON, authentication vs authorization, JWT, CORS, CRUD, pagination, and basic API security. You do not need to go extremely deep into advanced backend architecture unless the specific job requires it.