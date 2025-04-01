# RESTful API Design Best Practices

This guide outlines key principles and best practices for designing RESTful APIs that are scalable, maintainable, and developer-friendly.

## Core RESTful Principles

### Resource-Oriented

REST APIs are built around resources, which are any entity that can be stored, retrieved, created, updated, or deleted. Resources should be nouns, not verbs.

#### Good Resource Examples:

```
/users
/articles
/products
/orders
```

#### Poor Design (Using Verbs Instead of Nouns):

```
/getUsers
/createArticle
/updateProduct
```

### HTTP Methods for CRUD Operations

Use standard HTTP methods to perform CRUD operations on resources:

- **GET**: Retrieve a resource or collection of resources
- **POST**: Create a new resource
- **PUT**: Update a resource by replacing it entirely
- **PATCH**: Partially update a resource
- **DELETE**: Remove a resource

#### Example Endpoint Design:

```
GET /users                # List all users
GET /users/123            # Get user with ID 123
POST /users               # Create a new user
PUT /users/123            # Replace user 123
PATCH /users/123          # Partially update user 123
DELETE /users/123         # Delete user 123
```

### Statelessness

Each request from client to server must contain all the information needed to understand and process the request. The server should not store client state between requests.

- Authentication details should be included with each request
- Use tokens (JWT, OAuth) instead of server-side sessions
- Avoid storing client-specific data on the server between requests

## URI Design Best Practices

### Resource Naming Conventions

- Use plural nouns for collection resources: `/users` not `/user`
- Use concrete, specific names: `/articles` instead of `/content`
- Keep resource names lowercase and use hyphens for multi-word resources: `/product-categories`
- Avoid using file extensions: `/users` not `/users.json`

### Hierarchical Relationships

Represent resource relationships in the URL structure:

```
GET /users/123/orders            # Get all orders for user 123
GET /users/123/orders/456        # Get order 456 for user 123
POST /users/123/orders           # Create a new order for user 123
```

### Query Parameters for Filtering, Sorting, and Pagination

- Use query parameters (not URL paths) for filtering, sorting, and pagination
- Keep the base resource URL clean and use query parameters for modifications

```
GET /products?category=electronics       # Filter products by category
GET /products?sort=price&order=asc       # Sort products by price ascending
GET /products?limit=10&offset=20         # Pagination with offset
GET /products?page=2&per_page=20         # Pagination with page number
```

## Request and Response Handling

### Content Negotiation

Use HTTP headers for content negotiation:

- `Accept` header in requests to specify desired format
- `Content-Type` header in responses to indicate the format returned

```
# Request
GET /users/123
Accept: application/json

# Response
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "name": "John Doe",
  "email": "john@example.com"
}
```

### Status Codes

Use appropriate HTTP status codes to indicate the outcome of requests:

#### Success Codes
- **200 OK**: Request succeeded
- **201 Created**: Resource created successfully
- **204 No Content**: Request succeeded but no content returned (common for DELETE)

#### Client Error Codes
- **400 Bad Request**: Invalid request format or parameters
- **401 Unauthorized**: Authentication required
- **403 Forbidden**: Authentication succeeded but insufficient permissions
- **404 Not Found**: Resource not found
- **422 Unprocessable Entity**: Validation errors

#### Server Error Codes
- **500 Internal Server Error**: Server-side error occurred
- **503 Service Unavailable**: Server temporarily unavailable

### Error Response Format

Provide consistent, detailed error responses:

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid request parameters",
    "details": [
      {
        "field": "email",
        "message": "Must be a valid email address"
      },
      {
        "field": "password",
        "message": "Must be at least 8 characters long"
      }
    ]
  }
}
```

## Pagination, Filtering, and Sorting

### Pagination

Implement consistent pagination mechanisms:

#### Offset-Based Pagination

```
GET /articles?limit=20&offset=40
```

Response should include pagination metadata:

```json
{
  "data": [...],
  "pagination": {
    "total": 327,
    "limit": 20,
    "offset": 40,
    "next": "/articles?limit=20&offset=60",
    "previous": "/articles?limit=20&offset=20"
  }
}
```

#### Cursor-Based Pagination

Preferred for large datasets or when consistency during pagination is important:

```
GET /articles?limit=20&cursor=eyJpZCI6MTAwfQ==
```

### Filtering

Use query parameters for filtering with consistent naming conventions:

```
GET /products?category=electronics&price_min=100&price_max=500&in_stock=true
```

For complex filtering, consider a dedicated query parameter:

```
GET /products?filter={"category":"electronics","price":{"$gt":100,"$lt":500},"in_stock":true}
```

### Sorting

Implement consistent sorting with direction indicators:

```
GET /products?sort=price&order=asc
```

Or for multiple sort criteria:

```
GET /products?sort=price:asc,rating:desc
```

## Versioning Strategies

API versioning is essential for making non-backward-compatible changes. Common approaches include:

### URI Path Versioning

```
https://api.example.com/v1/users
https://api.example.com/v2/users
```

Pros: Very explicit, easy for clients to understand
Cons: Less adherent to REST principles, can lead to code duplication

### Header Versioning

```
GET /users
Accept: application/vnd.example.v2+json
```

Pros: Keeps URI space clean, follows HTTP content negotiation
Cons: Less visible, harder to test with browsers

### Query Parameter Versioning

```
GET /users?version=2
```

Pros: Easy to implement, doesn't require header modification
Cons: Less RESTful, pollutes query parameter space

## Authentication and Authorization

### Common Authentication Methods

#### Bearer Token Authentication (JWT, OAuth2)

```
GET /users/123
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

#### API Key Authentication

```
GET /users/123?api_key=abcdef123456
```

or

```
GET /users/123
X-API-Key: abcdef123456
```

### OAuth 2.0 Flow

For more complex authentication needs, implement OAuth 2.0:

1. Client registration
2. User authorization
3. Token exchange
4. API access with token

### Role-Based Access Control

Implement proper authorization checks:

```json
{
  "user": {
    "id": 123,
    "roles": ["editor", "commenter"],
    "permissions": ["articles:write", "comments:write", "comments:delete"]
  }
}
```

## Hypermedia and HATEOAS

Hypermedia as the Engine of Application State (HATEOAS) allows clients to navigate APIs through links instead of hardcoded URLs:

```json
{
  "id": 123,
  "name": "John Doe",
  "email": "john@example.com",
  "_links": {
    "self": { "href": "/users/123" },
    "orders": { "href": "/users/123/orders" },
    "update": { "href": "/users/123", "method": "PUT" },
    "delete": { "href": "/users/123", "method": "DELETE" }
  }
}
```

## Documentation Best Practices

### OpenAPI/Swagger Specification

Document your API using the OpenAPI (formerly Swagger) specification:

```yaml
openapi: 3.0.0
info:
  title: User API
  version: 1.0.0
paths:
  /users:
    get:
      summary: Returns a list of users
      responses:
        '200':
          description: A JSON array of user objects
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/User'
components:
  schemas:
    User:
      type: object
      properties:
        id:
          type: integer
        name:
          type: string
```

### Interactive Documentation

Provide interactive documentation with tools like:

- Swagger UI
- ReDoc
- Postman Collections

## Performance Optimization

### Response Field Filtering

Allow clients to request only the fields they need:

```
GET /users/123?fields=id,name,email
```

### Compression

Implement response compression to reduce bandwidth:

```
GET /users
Accept-Encoding: gzip, deflate
```

### Caching

Implement proper HTTP caching headers:

```
HTTP/1.1 200 OK
Cache-Control: max-age=3600, public
ETag: "33a64df551425fcc55e4d42a148795d9f25f89d4"
```

Support conditional requests:

```
GET /users/123
If-None-Match: "33a64df551425fcc55e4d42a148795d9f25f89d4"
```

### Batch Operations

Support batch operations to reduce requests:

```
POST /batch
Content-Type: application/json

{
  "operations": [
    { "method": "GET", "path": "/users/123" },
    { "method": "GET", "path": "/users/456" },
    { "method": "POST", "path": "/products", "body": { "name": "New Product" } }
  ]
}
```

## Security Considerations

### Security Headers

Implement security headers:

```
Strict-Transport-Security: max-age=31536000; includeSubDomains
Content-Security-Policy: default-src 'self'
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
X-XSS-Protection: 1; mode=block
```

### Input Validation

Validate all input parameters, both in URL and request body.

### Rate Limiting

Implement rate limiting to prevent abuse:

```
HTTP/1.1 429 Too Many Requests
Retry-After: 60
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 0
X-RateLimit-Reset: 1618884010
```

## Common Interview Questions about API Design

1. **How would you handle versioning in a RESTful API?**
   - Discuss different versioning strategies (URI, header, media type) and their trade-offs.

2. **What's the difference between PUT and PATCH requests?**
   - PUT replaces an entire resource, while PATCH applies partial modifications.

3. **How would you implement pagination in a RESTful API?**
   - Explain offset-based vs. cursor-based pagination and when to use each.

4. **How would you secure a RESTful API?**
   - Discuss authentication methods, HTTPS, CORS, input validation, and rate limiting.

5. **What status code would you return for [specific scenario]?**
   - Be prepared to discuss appropriate status codes for various error conditions.

6. **How would you handle search functionality in a RESTful API?**
   - Discuss query parameters, dedicated search endpoints, and filtering strategies.

7. **How can you make an API more performant?**
   - Discuss caching, compression, field filtering, batch operations, and database optimizations.

8. **What is HATEOAS and why might you implement it?**
   - Explain the concept of hypermedia controls and the benefits they provide for API evolution.