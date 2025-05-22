## Objective
To perform comprehensive API testing of the JSONPlaceholder service using Postman. This includes functional, schema validation, data-driven, performance, and security testing.

## Tools Used
- **Postman** (Environment, Collection Runner, Monitor)
- **CSV** for data-driven tests

## Scope
APIs tested for two main resources:
- `Posts`
- `Users`

## Environment Setup
1. **Environment Name**: `JSONPlaceholder Env`
2. **Variable**:
   - `baseUrl = https://jsonplaceholder.typicode.com`

## Collection Structure
- **Collection Name**: `JSONPlaceholder Assignment`
- **Folders**:
  - `Posts`
  - `Users`
- **Settings**: Enabled "Persist Variables"

## Manual API Testing

### `Posts` Folder

- `GET /posts`
  - ✅ Status 200
  - ✅ Response array length = 100
  - ✅ Schema validation

- `GET /posts/{id}`
  - ✅ Valid ID (e.g. 1) returns 200
  - ✅ Invalid ID (e.g. 9999) returns 404

- `POST /posts`
  - ✅ Created a post
  - ✅ Status 201 and response contains an `id`

- `PUT /posts/{id}`
  - ✅ Updated post title
  - ✅ Status 200 and correct title

- `DELETE /posts/{id}`
  - ✅ Status 200
  - ✅ Follow-up `GET` returns 404

### `Users` Folder

- `GET /users`
  - ✅ Status 200
  - ✅ Response array length ≥ 10

- `GET /users/{id}`
  - ✅ Valid ID (1) returns 200
  - ✅ Invalid ID (0) returns 404

## Schema Validation
Validated that `GET /posts` response includes:
- `userId` (integer)
- `id` (integer)
- `title` (string)
- `body` (string)

## Data-Driven Testing
- CSV File: `DataDriven_Posts.csv`
  ```
  id,expectedStatus
  1,200
  0,404
  9999,404
  ```
- Used in Collection Runner
- ✅ Dynamic assertions on status codes

## Pre-Request Script
```js
pm.environment.set('ts', new Date().toISOString());
```
Used `{{ts}}` for dynamic values in headers or queries.

## Security Testing
- SQL Injection Simulation:
  ```
  GET /posts?userId=' OR 1=1 --
  ```
  - ✅ No server-side errors or stack traces
  - ✅ Status code is 400 or 200

## Performance Monitoring
- Postman Monitor setup
- Scheduled monitoring with response time alerts

## Test Summary

| Test Type                   | Status  |
|----------------------------|---------|
| Status Code Verification   | ✅ Passed |
| Response Data Validation   | ✅ Passed |
| Schema Validation          | ✅ Passed |
| Data-Driven Testing        | ✅ Passed |
| Pre-Request Script         | ✅ Passed |
| Security Testing           | ✅ Passed |

## Deliverables
- ✅ Exported Postman Collection & Environment
- ✅ Published/Postman Collection Documentation
- ✅ Collection Runner & Monitor Reports (screenshots/HTML)
- ✅ Bug Reports via Postman Console

## Postman Collection Link
[Open in Postman Workspace](https://zoya-3668638.postman.co/workspace/zoya's-Workspace~75af44f9-5353-4682-8aba-0b528ec10e17/collection/44329802-16c16300-0278-48ed-8a3c-252dfc5b1704?action=share&creator=44329802&active-environment=44329802-4fcf0278-ba80-4f0c-9ce5-a9a8e2c5a79c)
