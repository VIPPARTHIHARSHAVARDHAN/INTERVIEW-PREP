# Backend Important Interview Questions

> Placement-focused backend interview questions with **direct answers**.  
> This file focuses only on the concepts that are most useful for fresher and entry-level software/backend interviews.

---

# 1. Backend Fundamentals

## Q1. What is backend development?

### Answer

Backend development is the server-side development of an application.

It mainly handles:

- Business logic
- APIs
- Database operations
- Authentication and authorization
- Request processing
- Communication with external services

Example:

```text
Frontend
   ↓
API Request
   ↓
Backend
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

## Q2. What happens when a user sends a request to a backend?

### Answer

A typical flow is:

```text
Client
  ↓
HTTP Request
  ↓
Web Server / Backend
  ↓
Route / Controller
  ↓
Business Logic
  ↓
Database / External Service
  ↓
Response
  ↓
Client
```

The backend receives the request, validates it, performs the required processing, accesses data if needed, and returns a response.

---

## Q3. What is an API?

### Answer

API stands for **Application Programming Interface**.

An API provides a way for different software components to communicate with each other.

For example:

```text
Frontend
   ↓
API
   ↓
Backend
   ↓
Database
```

The frontend can request data through the API without directly accessing the database.

---

## Q4. What is a REST API?

### Answer

A REST API is an API designed according to REST principles and commonly uses HTTP methods to work with resources.

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

## Q5. What is a server?

### Answer

A server is a system that receives requests, processes them, and sends responses.

Example:

```text
Client → Request → Server
Client ← Response ← Server
```

A backend application generally runs on a server.

---

## Q6. What is client-server architecture?

### Answer

Client-server architecture separates an application into clients that request services and servers that provide those services.

```text
Client
   ↓
Backend Server
   ↓
Database
```

For example, a browser can act as the client and a backend application can act as the server.

---

# 2. HTTP and REST

## Q7. What is HTTP?

### Answer

HTTP stands for **HyperText Transfer Protocol**.

It is a protocol used for communication between clients and servers.

REST APIs commonly use HTTP.

---

## Q8. What is HTTPS?

### Answer

HTTPS is HTTP communication protected using TLS encryption.

It helps protect data transmitted between the client and server.

```text
HTTP
→ Normal HTTP communication

HTTPS
→ HTTP + TLS security
```

---

## Q9. What are the main HTTP methods?

### Answer

The commonly used HTTP methods are:

```text
GET
POST
PUT
PATCH
DELETE
```

They are commonly associated with retrieving, creating, updating, partially updating, and deleting resources.

---

## Q10. What is GET?

### Answer

GET is generally used to retrieve data.

Example:

```http
GET /users/101
```

It requests information about user `101`.

---

## Q11. What is POST?

### Answer

POST is generally used to submit data or create a new resource.

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

## Q12. What is PUT?

### Answer

PUT is generally used for a complete update or replacement of a resource.

Example:

```http
PUT /users/101
```

---

## Q13. What is PATCH?

### Answer

PATCH is generally used for a partial update.

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

Only the specified field needs to be updated.

---

## Q14. What is DELETE?

### Answer

DELETE is generally used to remove a resource.

Example:

```http
DELETE /users/101
```

---

## Q15. PUT vs PATCH?

### Answer

| PUT | PATCH |
|---|---|
| Generally used for complete replacement/update | Generally used for partial update |
| Usually sends the complete resource representation | Can send only changed fields |
| Used when the resource is being fully updated | Used when only specific fields need changing |

---

## Q16. GET vs POST?

### Answer

| GET | POST |
|---|---|
| Generally retrieves data | Generally creates/submits data |
| Parameters commonly appear in URL/query | Data commonly appears in request body |
| Intended to be safe/read-only | Can change server state |

---

## Q17. What is CRUD?

### Answer

CRUD stands for:

```text
C → Create
R → Read
U → Update
D → Delete
```

Common REST mapping:

```text
POST       → Create
GET        → Read
PUT/PATCH  → Update
DELETE     → Delete
```

---

# 3. HTTP Status Codes

## Q18. What are HTTP status codes?

### Answer

HTTP status codes tell the client the result of a request.

They are grouped as:

```text
1xx → Informational
2xx → Success
3xx → Redirection
4xx → Client Error
5xx → Server Error
```

---

## Q19. What does 200 OK mean?

### Answer

`200 OK` means the request was successfully processed.

Example:

```http
GET /users/101
→ 200 OK
```

---

## Q20. What does 201 Created mean?

### Answer

`201 Created` indicates that a new resource was successfully created.

Example:

```http
POST /users
→ 201 Created
```

---

## Q21. What does 204 No Content mean?

### Answer

`204 No Content` indicates that the request was successfully processed but there is no response body.

It can be used for operations such as a successful deletion.

---

## Q22. What does 400 Bad Request mean?

### Answer

`400 Bad Request` means the request is invalid or cannot be processed because of invalid client-provided data.

Examples:

```text
Invalid JSON
Invalid input format
Missing required input
```

---

## Q23. What does 401 Unauthorized mean?

### Answer

`401 Unauthorized` generally means that valid authentication credentials were not provided.

Examples:

```text
Missing token
Invalid token
Expired credentials
```

---

## Q24. What does 403 Forbidden mean?

### Answer

`403 Forbidden` means the server understood the request but the client does not have permission to perform the requested operation.

Example:

```text
Authenticated normal user
        ↓
Attempts admin operation
        ↓
403 Forbidden
```

---

## Q25. What does 404 Not Found mean?

### Answer

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

## Q26. What does 500 Internal Server Error mean?

### Answer

`500 Internal Server Error` indicates that an unexpected error occurred on the server.

Examples:

```text
Unhandled application exception
Unexpected backend failure
```

---

## Q27. What is the difference between 401 and 403?

### Answer

```text
401
→ Authentication is missing or invalid.

403
→ The client is authenticated but does not have permission.
```

Easy way to remember:

```text
401 → "Who are you?"

403 → "I know who you are, but you cannot do this."
```

---

# 4. JSON and API Data

## Q28. What is JSON?

### Answer

JSON stands for **JavaScript Object Notation**.

It is a lightweight format commonly used to exchange structured data between clients and servers.

Example:

```json
{
    "id": 101,
    "name": "Ravi",
    "age": 22
}
```

---

## Q29. Why is JSON commonly used in REST APIs?

### Answer

JSON is:

- Lightweight
- Human-readable
- Easy to parse
- Supported by many programming languages
- Suitable for structured data

---

## Q30. What is a request body?

### Answer

A request body contains data sent from the client to the server.

Example:

```http
POST /users
Content-Type: application/json
```

```json
{
    "name": "Ravi",
    "age": 22
}
```

---

## Q31. What is a response body?

### Answer

A response body contains data returned by the server.

Example:

```json
{
    "id": 101,
    "name": "Ravi"
}
```

---

## Q32. What are HTTP headers?

### Answer

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
Content-Type: application/json
Authorization: Bearer <token>
```

---

# 5. REST API Design

## Q33. What is a REST resource?

### Answer

A resource represents an entity exposed by an API.

Examples:

```text
/users
/products
/orders
/employees
```

A specific resource can be identified using an ID:

```text
/users/101
/products/500
/orders/9001
```

---

## Q34. What is an endpoint?

### Answer

An endpoint is a specific URL through which a client accesses a resource or performs an operation.

Example:

```http
GET /users/101
```

Here:

```text
GET
→ HTTP method

/users/101
→ Endpoint path
```

---

## Q35. How should REST URLs generally be designed?

### Answer

REST URLs should generally represent resources using nouns.

Good:

```text
GET /users
GET /users/101
POST /users
DELETE /users/101
```

Less desirable action-based style:

```text
/getUsers
/createUser
/deleteUser
```

The HTTP method already represents the operation.

---

## Q36. How would you design a basic User API?

### Answer

A basic CRUD API could be:

```text
GET    /users
GET    /users/{id}
POST   /users
PUT    /users/{id}
PATCH  /users/{id}
DELETE /users/{id}
```

---

## Q37. What is a path parameter?

### Answer

A path parameter is a value included in the URL path to identify a resource.

Example:

```http
GET /users/101
```

Here:

```text
101
→ Path parameter
```

---

## Q38. What is a query parameter?

### Answer

A query parameter provides additional information such as filtering, searching, sorting, or pagination.

Example:

```http
GET /users?city=Hyderabad
```

Here:

```text
city=Hyderabad
→ Query parameter
```

---

## Q39. Path parameter vs query parameter?

### Answer

```text
Path parameter
→ Usually identifies a specific resource.

GET /users/101

Query parameter
→ Usually filters or modifies the retrieval.

GET /users?city=Hyderabad
```

---

## Q40. What is pagination?

### Answer

Pagination divides a large result set into smaller pages.

Example:

```http
GET /users?page=1&limit=20
```

Instead of returning thousands of records at once, the API returns a smaller set.

---

## Q41. Why is pagination important?

### Answer

Pagination helps:

- Reduce response size
- Reduce memory usage
- Reduce network traffic
- Improve response time
- Prevent unnecessarily large queries

---

# 6. Authentication and Authorization

## Q42. What is authentication?

### Answer

Authentication verifies the identity of a user or client.

Example:

```text
Username + Password
        ↓
Authentication
        ↓
User identified
```

---

## Q43. What is authorization?

### Answer

Authorization determines what an authenticated user or client is allowed to access or perform.

Example:

```text
User authenticated
       ↓
Check role/permission
       ↓
Allow or deny operation
```

---

## Q44. Authentication vs authorization?

### Answer

```text
Authentication
→ Who are you?

Authorization
→ What are you allowed to do?
```

Example:

```text
Login
→ Authentication

Accessing admin dashboard
→ Authorization
```

---

## Q45. What is a token?

### Answer

A token is a credential that can be sent with API requests to represent or authenticate a client after authentication.

Example:

```http
Authorization: Bearer <token>
```

---

## Q46. What is JWT?

### Answer

JWT stands for **JSON Web Token**.

It is a compact token format commonly used in authentication and authorization systems.

A JWT commonly contains:

```text
Header
Payload
Signature
```

---

## Q47. Explain the JWT authentication flow.

### Answer

```text
User Login
    ↓
Backend validates credentials
    ↓
Backend generates JWT
    ↓
Client receives token
    ↓
Client sends token with protected requests
    ↓
Backend validates token
    ↓
Request allowed/rejected
```

Example:

```http
Authorization: Bearer <JWT>
```

---

## Q48. Where should passwords be stored?

### Answer

Passwords should never be stored as plain text.

They should be stored using a strong password-hashing algorithm with an appropriate salt.

Conceptually:

```text
Password
   ↓
Password Hashing
   ↓
Stored Hash
```

During login, the supplied password is verified against the stored password hash.

---

## Q49. Why should HTTPS be used for authentication?

### Answer

HTTPS encrypts communication between the client and server using TLS.

Without HTTPS, sensitive information such as credentials or tokens could potentially be exposed while being transmitted.

---

# 7. Stateless REST APIs

## Q50. What does stateless mean in REST?

### Answer

Stateless means each request contains the information necessary for the server to process it.

The server does not depend on stored session state from a previous request to understand the current request.

Example:

```text
Request 1
→ Contains required authentication information

Request 2
→ Also contains required authentication information
```

---

## Q51. Why is statelessness useful?

### Answer

Stateless APIs are easier to scale because requests can be handled by different backend instances.

Example:

```text
             Load Balancer
                  ↓
          ┌───────┼───────┐
          ↓       ↓       ↓
       Server 1 Server 2 Server 3
```

A request does not necessarily need to return to the same server.

---

# 8. CORS

## Q52. What is CORS?

### Answer

CORS stands for **Cross-Origin Resource Sharing**.

It is a browser security mechanism that controls whether a web application from one origin can make requests to a different origin.

Example:

```text
Frontend:
https://frontend.example

Backend:
https://api.example
```

These are different origins.

The backend can specify which cross-origin requests are allowed.

---

## Q53. Is CORS an authentication mechanism?

### Answer

No.

CORS controls browser cross-origin access.

Authentication determines who the client/user is.

Authorization determines what that client/user is allowed to access.

---

# 9. API Security

## Q54. How would you secure a REST API?

### Answer

Important measures include:

```text
Use HTTPS
Use authentication
Implement authorization
Validate input
Hash passwords securely
Validate tokens
Use rate limiting
Protect secrets
Handle errors safely
```

---

## Q55. What is input validation?

### Answer

Input validation checks whether data received from a client satisfies expected rules.

Example:

```text
Age → Must be an integer
Email → Must have valid format
Price → Must not be negative
Name → Required
```

Backend validation is necessary even if the frontend performs validation.

---

## Q56. What is rate limiting?

### Answer

Rate limiting restricts the number of requests a client can make within a given period.

Example:

```text
100 requests per minute
```

If the client exceeds the limit, additional requests may be temporarily rejected.

---

## Q57. Why is rate limiting important?

### Answer

It helps:

- Prevent API abuse
- Protect server resources
- Control excessive traffic
- Reduce some automated attacks
- Maintain service availability

---

## Q58. Should an API expose internal errors?

### Answer

No.

Production APIs should not expose sensitive internal information such as:

```text
Database credentials
Secret keys
Internal stack traces
Infrastructure details
```

Instead, the API should return a safe error message while detailed information is logged securely on the backend.

---

# 10. API Error Handling

## Q59. How should an API handle invalid input?

### Answer

The backend should validate the request and return an appropriate client-error status.

For example:

```text
Invalid input
    ↓
400 Bad Request
```

The response should provide a useful but safe error message.

---

## Q60. What should happen if a requested user does not exist?

### Answer

The API would generally return:

```http
404 Not Found
```

Example:

```http
GET /users/101
```

If user `101` does not exist:

```http
404 Not Found
```

---

## Q61. What happens if the authentication token is invalid?

### Answer

The API would generally return:

```http
401 Unauthorized
```

because the request does not contain valid authentication credentials.

---

## Q62. What happens if an authenticated user tries to access an admin-only resource?

### Answer

If the user is authenticated but lacks the required permission:

```http
403 Forbidden
```

---

## Q63. What happens if the server encounters an unexpected exception?

### Answer

The API can return:

```http
500 Internal Server Error
```

The detailed exception should be logged securely on the server rather than exposed to the client.

---

# 11. API Testing

## Q64. What is API testing?

### Answer

API testing verifies whether an API behaves correctly for valid and invalid requests.

It can test:

```text
Status codes
Response data
Request validation
Authentication
Authorization
Error handling
Data correctness
```

---

## Q65. What is Postman?

### Answer

Postman is a tool commonly used to test APIs.

It allows developers to send HTTP requests such as:

```text
GET
POST
PUT
PATCH
DELETE
```

and inspect the returned responses.

---

## Q66. How would you test a REST API?

### Answer

I would check:

```text
1. HTTP method
2. URL
3. Headers
4. Request body
5. Authentication
6. Status code
7. Response body
8. Invalid input cases
9. Authorization cases
10. Edge cases
```

---

# 12. Backend Architecture

## Q67. What is a three-tier architecture?

### Answer

Three-tier architecture separates an application into:

```text
Presentation Layer
        ↓
Business Logic Layer
        ↓
Data Layer
```

For a typical web application:

```text
Frontend
   ↓
Backend / Business Logic
   ↓
Database
```

---

## Q68. What is the Controller-Service-Repository pattern?

### Answer

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

Handles database/data-access operations.

---

## Q69. Why separate controller, service, and repository?

### Answer

Separation of responsibilities makes the application:

- Easier to understand
- Easier to test
- Easier to maintain
- Easier to modify
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

# 13. API Versioning

## Q70. What is API versioning?

### Answer

API versioning allows an API to evolve without unexpectedly breaking existing clients.

Example:

```text
/api/v1/users
/api/v2/users
```

---

## Q71. Why is API versioning important?

### Answer

Different applications may depend on an existing API contract.

If a breaking change is introduced, older clients could stop working.

Versioning allows old and new API contracts to coexist.

---

# 14. Important Scenario Questions

## Q72. How would you design an API for an e-commerce application?

### Answer

I would identify the main resources first.

For example:

```text
/products
/users
/orders
/cart
```

Possible endpoints:

```text
GET    /products
GET    /products/{id}
POST   /products

GET    /orders
GET    /orders/{id}
POST   /orders

GET    /users/{id}
PATCH  /users/{id}
```

Authentication and authorization would protect operations that require a logged-in user or administrator.

---

## Q73. An API is returning thousands of records. How would you improve it?

### Answer

I would use:

```text
Pagination
Filtering
Sorting
Field selection where appropriate
Compression where appropriate
```

The API should avoid returning unnecessary data.

---

## Q74. An API is slow. How would you troubleshoot it?

### Answer

I would first identify the actual bottleneck.

I would investigate:

```text
Database queries
Database indexes
External API calls
Network latency
Large response payloads
Application processing
Caching opportunities
```

Then I would optimize the bottleneck rather than making assumptions.

---

## Q75. How would you handle a database failure while processing an API request?

### Answer

I would:

```text
1. Detect the database failure.
2. Log the error securely.
3. Avoid exposing internal database details.
4. Return an appropriate server-side error response.
5. Use retries only when safe and appropriate.
6. Ensure partial operations do not leave inconsistent data.
```

The exact response depends on the application and failure type.

---

## Q76. How would you handle duplicate user registration?

### Answer

I would enforce uniqueness at the database level for fields such as email where appropriate.

The backend should detect the conflict and return an appropriate response, commonly:

```http
409 Conflict
```

Example:

```text
POST /users

email = ravi@example.com

If the email already exists:
→ 409 Conflict
```

---

## Q77. How would you prevent unauthorized users from accessing another user's data?

### Answer

I would:

```text
1. Authenticate the user.
2. Identify the authenticated user.
3. Check whether that user owns the requested resource.
4. Check additional roles/permissions if required.
5. Reject unauthorized access.
```

For example, a user should not be able to access another user's private profile simply by changing:

```text
/users/101
```

to:

```text
/users/102
```

---

## Q78. What happens when a frontend calls `GET /users/101`?

### Answer

A typical flow is:

```text
Frontend
   ↓
GET /users/101
   ↓
Backend Router
   ↓
Authentication/Authorization
   ↓
Controller
   ↓
Service
   ↓
Repository
   ↓
Database
   ↓
User Data
   ↓
JSON Response
   ↓
Frontend
```

For example:

```json
{
    "id": 101,
    "name": "Ravi"
}
```

---

# 15. ⭐ Rapid-Fire Interview Questions

## Q79. What does REST stand for?

### Answer

**Representational State Transfer.**

---

## Q80. What is CRUD?

### Answer

```text
Create
Read
Update
Delete
```

---

## Q81. What HTTP method is generally used to retrieve data?

### Answer

```text
GET
```

---

## Q82. What HTTP method is generally used to create a resource?

### Answer

```text
POST
```

---

## Q83. What HTTP method is generally used for a complete update?

### Answer

```text
PUT
```

---

## Q84. What HTTP method is generally used for a partial update?

### Answer

```text
PATCH
```

---

## Q85. What HTTP method is generally used to delete a resource?

### Answer

```text
DELETE
```

---

## Q86. Which status code means successful request?

### Answer

```text
200 OK
```

---

## Q87. Which status code means resource created?

### Answer

```text
201 Created
```

---

## Q88. Which status code means bad request?

### Answer

```text
400 Bad Request
```

---

## Q89. Which status code is generally used for missing/invalid authentication?

### Answer

```text
401 Unauthorized
```

---

## Q90. Which status code is generally used when the client lacks permission?

### Answer

```text
403 Forbidden
```

---

## Q91. Which status code means resource not found?

### Answer

```text
404 Not Found
```

---

## Q92. Which status code generally indicates an unexpected server error?

### Answer

```text
500 Internal Server Error
```

---

## Q93. What is JWT?

### Answer

JWT is a compact token format commonly used for authentication and authorization.

---

## Q94. What is CORS?

### Answer

CORS is a browser security mechanism that controls cross-origin requests.

---

## Q95. What is pagination?

### Answer

Pagination divides a large result set into smaller pages.

---

## Q96. What is rate limiting?

### Answer

Rate limiting restricts the number of requests a client can make within a specified period.

---

# 16. ⭐ Top 20 Questions to Prepare First

If interview preparation time is limited, prioritize these questions:

```text
1. What is backend development?
2. What is an API?
3. What is REST API?
4. What is HTTP?
5. HTTP vs HTTPS?
6. What are GET, POST, PUT, PATCH and DELETE?
7. PUT vs PATCH?
8. What is CRUD?
9. What are HTTP status codes?
10. 401 vs 403?
11. What is JSON?
12. What are path and query parameters?
13. What is pagination?
14. What is authentication?
15. What is authorization?
16. Authentication vs authorization?
17. What is JWT?
18. What is CORS?
19. How do you secure a REST API?
20. How would you design a basic CRUD API?
```

---

# 17. ⭐ Interview Answer: Explain REST API in One Minute

### Answer

> "A REST API is an API designed according to REST principles that allows clients and servers to communicate, usually over HTTP. In REST, data is represented as resources, such as users or products, and HTTP methods like GET, POST, PUT, PATCH, and DELETE are used to interact with those resources. For example, `GET /users/101` retrieves a user, while `POST /users` can create a new user. REST APIs are commonly stateless, meaning each request contains the information required to process it."

---

# 18. ⭐ Interview Answer: Explain Authentication vs Authorization

### Answer

> "Authentication verifies the identity of a user, while authorization determines what that authenticated user is allowed to access. For example, logging into an application with a username and password is authentication. After login, checking whether the user has permission to access an admin page is authorization."

---

# 19. ⭐ Interview Answer: Explain JWT

### Answer

> "JWT stands for JSON Web Token. It is commonly used for authentication. After a user successfully logs in, the backend can generate a JWT and return it to the client. The client sends the token with subsequent protected requests, usually through the Authorization header. The backend validates the token before allowing access."

---

# 20. ⭐ Interview Answer: Explain the Backend Request Flow

### Answer

> "When a client sends a request, it first reaches the backend through an HTTP endpoint. The backend validates the request and authentication, then the controller handles the request and passes it to the service layer. The service applies business logic and may call the repository to access the database. Finally, the backend sends a response with an HTTP status code and usually JSON data."

---

# 21. Final Revision Checklist

```text
BACKEND BASICS
☐ Backend development
☐ Client-server architecture
☐ Server
☐ API
☐ Business logic

HTTP
☐ HTTP
☐ HTTPS
☐ Request
☐ Response
☐ Headers
☐ Request body
☐ Response body

HTTP METHODS
☐ GET
☐ POST
☐ PUT
☐ PATCH
☐ DELETE
☐ PUT vs PATCH
☐ GET vs POST

REST
☐ REST
☐ REST API
☐ Resources
☐ Endpoints
☐ Statelessness
☐ CRUD
☐ REST URL design

STATUS CODES
☐ 200
☐ 201
☐ 204
☐ 400
☐ 401
☐ 403
☐ 404
☐ 409
☐ 500

API DATA
☐ JSON
☐ Path parameters
☐ Query parameters
☐ Pagination

SECURITY
☐ Authentication
☐ Authorization
☐ Authentication vs Authorization
☐ JWT
☐ HTTPS
☐ CORS
☐ Input validation
☐ Rate limiting
☐ Secure error handling

ARCHITECTURE
☐ Three-tier architecture
☐ Controller
☐ Service
☐ Repository
☐ Database

PRACTICAL
☐ API testing
☐ Postman
☐ API versioning
☐ API error handling
☐ CRUD API design
☐ Troubleshooting a slow API
☐ Securing an API
```

---

# 22. Final Placement Priority

## Must Know Very Well

```text
API
REST API
HTTP/HTTPS
GET/POST/PUT/PATCH/DELETE
CRUD
Status Codes
JSON
REST Resources
Endpoints
Path Parameters
Query Parameters
Authentication
Authorization
JWT
CORS
Statelessness
Pagination
API Security
```

## Know at a Basic Level

```text
Controller-Service-Repository
Three-Tier Architecture
Rate Limiting
API Versioning
API Testing
Postman
Error Handling
```

> **Placement goal:** You should be able to explain the above concepts in simple words, give a small example, and answer basic scenario questions. For fresher interviews, strong fundamentals are more important than going very deep into advanced backend architecture.