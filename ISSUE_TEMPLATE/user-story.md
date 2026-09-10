**As a** developer of the e-commerce platform  
**I need** REST API endpoints to read, update, delete, and list existing customer accounts  
**So that** other microservices can manage customer accounts reliably and consistently

### Details and Assumptions

* The database model for customer accounts already exists.
* The Flask application and the REST endpoint for creating a customer account already exist.
* The new functionality will be integrated into the existing Flask application.
* Customer accounts are identified by a unique `account_id`.
* The API uses JSON for requests and responses.
* A single account is retrieved using `GET /accounts/{account_id}`.
* All accounts are retrieved using `GET /accounts`.
* Account updates use `PATCH /accounts/{account_id}` so that individual fields can be changed.
* Accounts are deleted using `DELETE /accounts/{account_id}`.
* A request for a non-existent account returns `404 Not Found`.
* Invalid or incomplete input returns an appropriate error status, such as `400 Bad Request`.
* Development and testing take place in an online lab environment.
* Before implementation, the project structure, dependencies, database connection, and existing account-creation endpoint are reviewed.

### Acceptance Criteria

#### Retrieve a customer account

```gherkin
Given an existing customer account with a valid account_id
When a GET request is sent to /accounts/{account_id}
Then the customer account is returned as JSON with HTTP 200 OK
```

```gherkin
Given no customer account exists with the specified account_id
When a GET request is sent to /accounts/{account_id}
Then HTTP 404 Not Found is returned with a clear error message
```

#### List customer accounts

```gherkin
Given multiple customer accounts exist in the database
When a GET request is sent to /accounts
Then the customer accounts are returned as a JSON list with HTTP 200 OK
```

```gherkin
Given no customer accounts exist in the database
When a GET request is sent to /accounts
Then an empty JSON list is returned with HTTP 200 OK
```

#### Update a customer account

```gherkin
Given an existing customer account with a valid account_id
And the submitted update data is valid
When a PATCH request is sent to /accounts/{account_id}
Then the customer account is updated
And the updated account data is returned as JSON with HTTP 200 OK
```

```gherkin
Given an existing customer account with a valid account_id
And the submitted update data is invalid or incomplete
When a PATCH request is sent to /accounts/{account_id}
Then the customer account is not changed
And HTTP 400 Bad Request is returned with a clear error message
```

```gherkin
Given no customer account exists with the specified account_id
When a PATCH request is sent to /accounts/{account_id}
Then HTTP 404 Not Found is returned with a clear error message
```

#### Delete a customer account

```gherkin
Given an existing customer account with a valid account_id
When a DELETE request is sent to /accounts/{account_id}
Then the customer account is permanently deleted
And HTTP 204 No Content is returned
```

```gherkin
Given no customer account exists with the specified account_id
When a DELETE request is sent to /accounts/{account_id}
Then HTTP 404 Not Found is returned with a clear error message
```

#### Development environment and quality

```gherkin
Given the application is running in the online lab environment
When the project dependencies and database connection have been configured
Then the Flask application can be started
And the existing and new REST endpoints can be tested
```

```gherkin
Given the REST endpoints are tested with valid and invalid input
When the test cases are executed
Then the endpoints return the expected HTTP status codes
And the database remains unchanged when validation fails
```
