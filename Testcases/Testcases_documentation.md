# Testcase documentation
## Table of contents
### 1.Create request (POST method)
#### 1.1 Successful POST request
#### 1.2 Successful POST response
#### 1.3 API responds within the expected threshold
#### 1.4 API response contains the expected header
#### 1.5 Extract created item id
### 2.Create request - no Body (POST method)
#### 2.1 Unsuccessful POST request - missing body
#### 2.2 POST response test - no body
#### 2.3 API response contains the expected header
### 3.Create request - syntax error (POST method)
#### 3.1 Unsuccessful POST request - syntax error
#### 3.2 POST response test - syntax error
#### 3.3 API response contains the expected header
### 4.Read all request - (GET method)
#### 4.1 Successful GET request
#### 4.2 Response has a JSON body
#### 4.3 API responds within the expected threshold
#### 4.4 API response contains the expected header
### 5.Read all request - non existing endpoint (GET method)
#### 5.1 Unsuccessful GET request - non existing endpoint
#### 5.2 Body is string
#### 5.3 API response contains the expected header
### 6.Read request by id (GET method)
#### 6.1 Response has a JSON body
#### 6.2 Check response properties
### 7.Read request by id - non existing id (GET method)
#### 7.1 Unsuccessful GET request - non existing id
#### 7.2 GET response test - non existing id
#### 7.3 API response contains the expected header
### 8.Update request by id (PUT method)
#### 8.1 Successful PUT request
#### 8.2 API responds within the expected threshold
### 9.Read request by id after update (GET method)
#### 9.1 GET response has a JSON body
#### 9.2 Check updated property
### 10.Update request by id - non existing id (PUT method)
#### 10.1 Unsuccessful PUT request - non existing id
#### 10.2 PUT response test - non existing id
#### 10.3 API response contains the expected header
### 11.Update request by id - syntax error (PUT method)
#### 11.1 Unsuccessful PUT request - syntax error
#### 11.2 PUT response test - syntax error
#### 11.3 API response contains the expected header
### 12.Delete request by id (DELETE method)
#### 12.1 Successful DELETE request
#### 12.2 API responds within the expected threshold
### 13.Read request by id after delete (GET method)
#### 13.1 Unsuccessful GET request - non existing id
#### 13.2 GET response test - non existing id
#### 13.3 API response contains the expected header
### 14.Delete request by id - non existing id (DELETE method)
#### 14.1 Unsuccessful DELETE request - non existing id
#### 14.2 DELETE response test - non existing id
#### 14.3 API response contains the expected header




## Testcases

### [1.1] Successful POST request
#### Description
POST method response is tested for status code.
#### Precondition
POST method request needs to have body defined.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("Successful POST request", () => {
    const expectedStatusCodes = [201,202];
  pm.expect(pm.response.code).to.be.oneOf(expectedStatusCodes)
});

#### Expected Result
Status 201 Created is set.

### [1.2] Successful POST response
#### Description
POST method response is tested to have required properties with correct data types.
#### Precondition
POST method request needs to have body defined.

#### Test Execution
Run request manually ("Send") or as a part of collection.

const jsonData = pm.response.json();
pm.test("Successful POST Response", () => {
  pm.expect(jsonData).to.be.an("object");
  pm.expect(jsonData.name).to.be.a("string");
  pm.expect(jsonData.description).to.be.a("string");
  pm.expect(jsonData.activation_date).to.be.a("string");
  pm.expect(jsonData.repeat).to.be.a("string");
  pm.expect(jsonData.status).to.be.a("string");
  pm.expect(jsonData._id).to.be.a("string");
});

#### Expected Result
Response body has correct properties set.

### [1.3] API responds within the expected threshold
#### Description
POST method API response is tested to be within expected threshold
#### Precondition
POST method request needs to have body defined.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("API responds within the expected treshhold", () => {
  // set the response time in milliseconds
  const expectedTimeInMilliseconds = 500;

  pm.expect(pm.response.responseTime).to.be.lessThan(
    expectedTimeInMilliseconds + 1);
});

#### Expected Result
API responds within expected threshold.

### [1.4] API response contains the expected header
#### Description
POST method API response is tested to have header Content-Type with value application/json.
#### Precondition
POST method request needs to have body defined.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("API response contains the expected header", () => {
  pm.response.to.have.header("Content-Type", "application/json; charset=utf-8");
});

#### Expected Result
API response contains the expected header and value.


### [1.5] Extract created item id
#### Description
POST method API response is tested to have id set.
#### Precondition
POST method request needs to have body defined.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("Extract created item id", function(){
var jsonData = JSON.parse(responseBody);
pm.environment.set("id", jsonData._id);
});

#### Expected Result
API response contains the expected header and value. Environment variable id is dynamically set.

### [2.1] Unsuccessful POST request - missing body
#### Description
POST method request is sent without body where expected status code should be 415.
#### Precondition
POST method request body is not defined.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("Unsuccessful POST request - missing body", () => {
  pm.response.to.have.status(415);
});

#### Expected Result
API response contains expected status 415.

### [2.2] POST response test - no body
#### Description
POST method request is sent without body. Response is checked for correct properties and values.
#### Precondition
POST method request body is not defined.

#### Test Execution
Run request manually ("Send") or as a part of collection.

const jsonData = pm.response.json();
pm.test("POST response test - no body", () => {
  pm.expect(jsonData).to.be.an("object");
  pm.expect(jsonData.type).to.be.a("string");
  pm.expect(jsonData.title).to.be.a("string");
  pm.expect(jsonData.title).to.eql("Unsupported Media Type");
  pm.expect(jsonData.status).to.be.an("number");
  pm.expect(jsonData.traceId).to.be.a("string");
});

#### Expected Result
API response contains expected properties and values.

### [2.3] API response contains the expected header
#### Description
POST method request is sent without body. Response is checked to have Content-Type header with value application/problem+json.
#### Precondition
POST method request body is not defined.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("API response contains the expected header", () => {
  pm.response.to.have.header("Content-Type", "application/problem+json; charset=utf-8");
});

#### Expected Result
API response contains expected header with correct value.

### [3.1] Unsuccessful POST request - syntax error
#### Description
POST method request is sent with body where syntax error is present on property and status error code 400 is expected.
#### Precondition
POST method request body is defined with syntax error.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("Unsuccessful POST request - syntax error", () => {
  pm.response.to.have.status(400);
});

#### Expected Result
API response contains expected status 400.


### [3.2] POST response test - syntax error
#### Description
POST method request is sent with body where syntax error is present on property, response body is tested for correct properties and values.
#### Precondition
POST method request body is defined with syntax error.

#### Test Execution
Run request manually ("Send") or as a part of collection.

const jsonData = pm.response.json();
pm.test("POST response test - syntax error", () => {
  pm.expect(jsonData).to.be.an("object");
  pm.expect(jsonData.errors).to.have.nested.property('repeat');
  pm.expect(jsonData.title).to.be.a("string");
  pm.expect(jsonData.title).to.eql("One or more validation errors occurred.");
  pm.expect(jsonData.status).to.be.a("number");
  pm.expect(jsonData.traceId).to.be.a("string");
});

#### Expected Result
API response contains expected properties with correct values.

### [3.3] API response contains the expected header
#### Description
POST method request is sent with body where syntax error is present on property. Response is checked to have Content-Type header with value application/problem+json.
#### Precondition
POST method request body is defined with syntax error.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("API response contains the expected header", () => {
  pm.response.to.have.header("Content-Type", "application/problem+json; charset=utf-8");
});

#### Expected Result
API response contains expected header with correct value.

### [4.1] Successful GET request
#### Description
GET method response is tested for status code.
#### Precondition
Existing endpoint is read.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("Successful GET request", function(){
    pm.response.to.have.status(200);
});

#### Expected Result
Status 200 OK is set.

### [4.2] Response has a JSON body
#### Description
GET method response is tested to have body.
#### Precondition
Existing endpoint is read.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("Response has a JSON body", function () {
    pm.response.to.be.json;
});

#### Expected Result
Body is present in response.

### [4.3] API responds within the expected threshold
#### Description
GET method response is tested to be within expected time threshold.
#### Precondition
Existing endpoint is read.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("API responds within the expected treshhold", () => {
  // set the response time in milliseconds
  const expectedTimeInMilliseconds = 500;

  pm.expect(pm.response.responseTime).to.be.lessThan(
    expectedTimeInMilliseconds + 1);
});

#### Expected Result
API responded within expected time threshold.

### [4.4] API response contains the expected header
#### Description
GET method response is tested to contain Content-Type header with value application/json.
#### Precondition
Existing endpoint is read.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("API response contains the expected header", () => {
  pm.response.to.have.header("Content-Type", "application/json; charset=utf-8");
});

#### Expected Result
API response contains correct header and value.

### [5.1] Unsuccessful GET request - non existing endpoint
#### Description
GET method response is checked when endpoint which is read does not exist. Status 400 is expected.
#### Precondition
Endpoint does not exist.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("Unsuccessful GET request - non existing endpoint", () => {
  pm.response.to.have.status(400);
});

#### Expected Result
Status code 400 is set.

### [5.2] Body is string
#### Description
GET method response body is checked when endpoint which is read does not exist. Body shall be type string.
#### Precondition
Endpoint does not exist.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("Body is string", function () {
  pm.response.to.have.body("Endpoint doesn\'t exist.");
});

#### Expected Result
String is present in response body.

### [5.3] API response contains the expected header
#### Description
GET method response body is checked when endpoint which is read does not exist. Header Content-Type shall be present with value text/plain.
#### Precondition
Endpoint does not exist.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("API response contains the expected header", () => {
  pm.response.to.have.header("Content-Type", "text/plain; charset=utf-8");
});

#### Expected Result
Header with correct value is present.

### [6.1] Response has a JSON body
#### Description
GET method response body is checked when read request for single id is executed.
#### Precondition
Existing endpoint and id is read.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("Response has a JSON body", function () {
    pm.response.to.be.json;
});

#### Expected Result
Response contains body.

### [6.2] Check response properties
#### Description
GET method response body is checked when read request for single id is executed. All created properties shall be available and correct data type.
#### Precondition
Existing endpoint and id is read.

#### Test Execution
Run request manually ("Send") or as a part of collection.

const jsonData = pm.response.json();
pm.test("Check response properties", () => {
  pm.expect(jsonData).to.be.an("object");
  pm.expect(jsonData.name).to.be.a("string");
  pm.expect(jsonData.description).to.be.a("string");
  pm.expect(jsonData.activation_date).to.be.a("string");
  pm.expect(jsonData.repeat).to.be.a("string");
  pm.expect(jsonData.status).to.be.a("string");
  pm.expect(jsonData._id).to.be.a("string");
});

#### Expected Result
Response body properties are available and correct.

### [7.1] Unsuccessful GET request - non existing id
#### Description
GET method status is checked when read request for non existing id is executed. Status shall be 404.
#### Precondition
Existing endpoint and non existing id is read.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("Unsuccessful GET request - non existing id", () => {
  pm.response.to.have.status(404);
});

#### Expected Result
Set status is 404 Not Found. 

### [7.2] GET response test - non existing id
#### Description
GET method response body is checked when read request for non existing id is executed.
#### Precondition
Existing endpoint and non existing id is read.

#### Test Execution
Run request manually ("Send") or as a part of collection.

const jsonData = pm.response.json();
pm.test("GET response test - non existing id", () => {
  pm.expect(jsonData).to.be.an("object");
  pm.expect(jsonData.type).to.be.a("string");
  pm.expect(jsonData.title).to.be.a("string");
  pm.expect(jsonData.title).to.eql("Not Found");
  pm.expect(jsonData.status).to.be.an("number");
  pm.expect(jsonData.status).to.eql(404);
  pm.expect(jsonData.traceId).to.be.a("string");
});

#### Expected Result
Response body properties matches expected values. 

### [7.3] API response contains the expected header
#### Description
GET method response body is checked to contain "Content-Type" header with value "application/problem+json".
#### Precondition
Existing endpoint and non existing id is read.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("API response contains the expected header", () => {
  pm.response.to.have.header("Content-Type", "application/problem+json; charset=utf-8");
});

#### Expected Result
Response body header is available with correct value. 

### [8.1] Successful PUT request
#### Description
PUT method status code is checked. Status 200 OK is expected.
#### Precondition
Body is defined with updated value for property.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("Successful PUT request", () => {
   pm.response.to.have.status(200);
});

#### Expected Result
Set status is 200 OK.

### [8.2] API responds within the expected threshold
#### Description
PUT method response time threshold is checked.
#### Precondition
Body is defined with updated value for property.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("API responds within the expected treshhold", () => {
  // set the response time in milliseconds
  const expectedTimeInMilliseconds = 500;

  pm.expect(pm.response.responseTime).to.be.lessThan(
    expectedTimeInMilliseconds + 1);
});

#### Expected Result
API responds within expected time threshold.

### [9.1] GET response has a JSON body
#### Description
GET method response contains body.
#### Precondition
Body property was updated with PUT method.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("GET response has a JSON body", function () {
    pm.response.to.be.json;
});

#### Expected Result
Response body is available.

#### Expected Result
API responds within expected time threshold.

### [9.2] Check updated property
#### Description
GET method response body contains updated value for property.
#### Precondition
Body property was updated with PUT method.

#### Test Execution
Run request manually ("Send") or as a part of collection.

const jsonData = pm.response.json();
pm.test("Check updated property", () => {
  pm.expect(jsonData).to.be.an("object");
  pm.expect(jsonData.name).to.be.a("string");
  pm.expect(jsonData.description).to.be.a("string");
  pm.expect(jsonData.activation_date).to.be.a("string");
  pm.expect(jsonData.repeat).to.be.a("string");
  pm.expect(jsonData.status).to.be.a("string");
  pm.expect(jsonData.status).to.eql("completed");
  pm.expect(jsonData._id).to.eql(pm.environment.get("id"));
});

#### Expected Result
Response body property is correctly updated.

### [10.1] Unsuccessful PUT request - non existing id
#### Description
PUT method status code is checked when id which is updated does not exist.
#### Precondition
Id does not exist.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("Unsuccessful PUT request - non existing id", () => {
  pm.response.to.have.status(404);
});

#### Expected Result
Status code is 404 Not Found.

#### Expected Result
Response body property is correctly updated.

### [10.2] PUT response test - non existing id
#### Description
PUT method response body is checked when id which is updated does not exist.
#### Precondition
Id does not exist.

#### Test Execution
Run request manually ("Send") or as a part of collection.

const jsonData = pm.response.json();
pm.test("PUT response test - non existing id", () => {
  pm.expect(jsonData).to.be.an("object");
  pm.expect(jsonData.type).to.be.a("string");
  pm.expect(jsonData.title).to.be.a("string");
  pm.expect(jsonData.title).to.eql("Not Found");
  pm.expect(jsonData.status).to.be.an("number");
  pm.expect(jsonData.status).to.eql(404);
  pm.expect(jsonData.traceId).to.be.a("string");
});

#### Expected Result
Response body properties and values are as expected.

### [10.3] API response contains the expected header
#### Description
PUT method response body is checked to contain Content-Type header with value application/problem+json.
#### Precondition
Id does not exist.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("API response contains the expected header", () => {
  pm.response.to.have.header("Content-Type", "application/problem+json; charset=utf-8");
});

#### Expected Result
Response body header is correct.

### [11.1] Unsuccessful PUT request - syntax error
#### Description
PUT method status code is checked when body which is updated contains syntax error.
#### Precondition
Body contains syntax error.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("Unsuccessful PUT request - syntax error", () => {
  pm.response.to.have.status(400);
});

#### Expected Result
Status code is 400 Bad Request.

### [11.2] PUT response test - syntax error 
#### Description
PUT method response body is checked when body contains syntax error.
#### Precondition
Body contains syntax error.

#### Test Execution
Run request manually ("Send") or as a part of collection.

const jsonData = pm.response.json();
pm.test("PUT response test - syntax error", () => {
  pm.expect(jsonData).to.be.an("object");
  pm.expect(jsonData.errors).to.have.nested.property('status');
  pm.expect(jsonData.title).to.be.a("string");
  pm.expect(jsonData.title).to.eql("One or more validation errors occurred.");
  pm.expect(jsonData.status).to.be.a("number");
  pm.expect(jsonData.traceId).to.be.a("string");

#### Expected Result
Response body properties and values are as expected.

### [11.3] API response contains the expected header
#### Description
PUT method response body is checked to contain Content-Type header with value application/problem+json.
#### Precondition
Body contains syntax error.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("API response contains the expected header", () => {
  pm.response.to.have.header("Content-Type", "application/problem+json; charset=utf-8");
});

#### Expected Result
Response body header is correct.

### [12.1] Successful DELETE request
#### Description
DELETE method status code is checked.
#### Precondition
Existing id is used.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("Successful DELETE request", () => {
    pm.response.to.have.status(200);
});

#### Expected Result
Status code is 200 OK.

### [12.2] API responds within the expected threshold
#### Description
DELETE method is checked to be within expected time threshold.
#### Precondition
Existing id is used.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("API responds within the expected treshhold", () => {
  // set the response time in milliseconds
  const expectedTimeInMilliseconds = 500;

  pm.expect(pm.response.responseTime).to.be.lessThan(
    expectedTimeInMilliseconds + 1);
});

#### Expected Result
API response is within threshold.

### [13.1] Unsuccessful GET request - non existing id
#### Description
GET method status is checked when read request is executed for deleted id. Status shall be 404.
#### Precondition
Existing endpoint and deleted id is read.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("Unsuccessful GET request - non existing id", () => {
  pm.response.to.have.status(404);
});

#### Expected Result
Set status is 404 Not Found. 

### [13.2] GET response test - non existing id
#### Description
GET method response body is checked when read request for deleted  id is executed.
#### Precondition
Existing endpoint and deleted id is read.

#### Test Execution
Run request manually ("Send") or as a part of collection.

const jsonData = pm.response.json();
pm.test("GET response test - non existing id", () => {
  pm.expect(jsonData).to.be.an("object");
  pm.expect(jsonData.type).to.be.a("string");
  pm.expect(jsonData.title).to.be.a("string");
  pm.expect(jsonData.title).to.eql("Not Found");
  pm.expect(jsonData.status).to.be.an("number");
  pm.expect(jsonData.status).to.eql(404);
  pm.expect(jsonData.traceId).to.be.a("string");
});

#### Expected Result
Response body properties matches expected values. 

### [13.3] API response contains the expected header
#### Description
GET method response body is checked to contain "Content-Type" header with value "application/problem+json" when reading deleted id.
#### Precondition
Existing endpoint and deleted id is read.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("API response contains the expected header", () => {
  pm.response.to.have.header("Content-Type", "application/problem+json; charset=utf-8");
});

#### Expected Result
Response body header is available with correct value. 

### [14.1] Unsuccessful DELETE request - non existing id
#### Description
DELETE method status is checked when delete request is executed for non existing id. Status shall be 404.
#### Precondition
Id to be deleted does not exist.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("Unsuccessful DELETE request - non existing id", () => {
  pm.response.to.have.status(404);
});

#### Expected Result
Set status is 404 Not Found. 

### [14.2] DELETE response test - non existing id
#### Description
DELETE method response body is checked when delete request for non existing id is executed.
#### Precondition
Id to be deleted does not exist.

#### Test Execution
Run request manually ("Send") or as a part of collection.

const jsonData = pm.response.json();
pm.test("DELETE response test - non existing id", () => {
  pm.expect(jsonData).to.be.an("object");
  pm.expect(jsonData.type).to.be.a("string");
  pm.expect(jsonData.title).to.be.a("string");
  pm.expect(jsonData.title).to.eql("Not Found");
  pm.expect(jsonData.status).to.be.an("number");
  pm.expect(jsonData.status).to.eql(404);
  pm.expect(jsonData.traceId).to.be.a("string");
});

#### Expected Result
Response body properties matches expected values. 

### [14.3] API response contains the expected header
#### Description
DELETE method response body is checked to contain "Content-Type" header with value "application/problem+json" when trying to delete non existing id.
#### Precondition
Id to be deleted does not exist.

#### Test Execution
Run request manually ("Send") or as a part of collection.

pm.test("API response contains the expected header", () => {
  pm.response.to.have.header("Content-Type", "application/problem+json; charset=utf-8");
});

#### Expected Result
Response body header is available with correct value. 


