# CardApp - Wharf API Test Project

This is a project to develop a workspace for test automation of CardApp API for Wharf

- API Consumer Client: `Wharf`
- API Producer Company: `CardApp`
- API Document version: `1.3`
- API Document Writer: `Even`

- The readme is written by `Simon CHAM`

## Project Organization

This project is implemented with `Postman`. For the sake of reusability, the project is organized as the following:

|Item| Description|
|--|--|
|Test Scripts| All are written with `Postman`.|
|Test Cases| All test scripts for a test case is grouped in one `Postman`'s `collection`.
|Test Data| Test data for a Test Case are stored in a separated test data file (in `csv` or `json` format).
|Environment| All runtime variables are stored in `Postman`'s `environment`s. All environment variable names are in `UPPER_CASE`. The environment is divided by site and language, so we will have `SIT EN`, `SIT HK` , `UAT EN`, `UAT HK` etc.

Directory Structure:

|path|description|
|--|--|
|`<project>\collections\`| the folder contains all `collection`s
|`<project>\environments\`| the folder contains all `environment`s
`<project>\data\`| the folder contains all test data set
|`<project>\lib\`| util scripts for preparation of test data.
|`<project>\files`| files for test upload or download api.
|`<project>\readme.md`| this document
|`<project>\package.json`| the node.js package.json file

## Setup of the Postman Workspace

- Unzip the project zip file.
- Create a new Workspace in Postman for this project.
- Import all files in the folder `collections\` to Postman **collections**
- Import all files in the folder `environments\` to Postman **environments**  

(Optional) if you want to use the util scripts in `lib\` or plan for automatic execution of tests, do the following:

- You already have `Node.js` (version 12 or higher) installed.
- In the directory `<project>\`, execute command `npm i .` to install the dependencies defined in `package.json`.

## Environment Variables

To prepare an environment for running the tests, the following variables should be defined.

|Variable| Description | Examples|
|--|--|--|
|`BASE_URL`| The base URL of the api endpoints.
|`UI_URL`| The corresponding portal URL for reference.
|`USER_NAME`| The default valid user name to perform the tests.
|`USER_PASSWORD`| The password of `USER_NAME`.
|`MASTER_SECRET`| The master secret in the header of request for accessing the APIs.
|`APP_ESTATE_ID`| The default `AppEstateId` required by the APIs
|`DEVICE_INFO`| The default `DeviceInfo` required by the APIs
|`CLIENT_TYPE`| The default `ClientType` required by the APIs
|`LANGUAGE`| The default `Language`. `1` - EN, `2` - TC, `3` - SC |
|`RESPONSE_TIME`| The max threshold of a request response time. A request should be classified as a failure of quality of performance if its response is over this value.
|`INVALID_USER_NAME`| The default invalid user name
|`INVALID_USER_PASSWORD`| The password of `INVALID_USER_NAME`
|`INVALID_USER_TOKEN`| The default invalid user token|
|`_SALT`|
|`_HASH`|
|`_USER_ID`|
|`_USER_TOKEN`|
|`_COMMON_TEST_HAPPY`| The Postman test script for happy paths (cases).
|`_COMMON_TEST_UNHAPPY`| The Postman test script for unhappy paths.
|`_POST_SALTING`| The process with algorithm to generate MD5 hash for sign-in.
|`_POST_TOKENIZE`| The process to keep the user token in environment if sign-in success.
|`_PRESET_HEADERS`| The process to preset the request header with `MASTER_SECRET`.
|`_HELPER`| Define a helper function of algorithm to generate MD5 hash

## Test Data

This project is designed for *Data Driven Testing (DDT)*.

|Test Case| Test Data|
|--|--|
|1.1  Login with valid FMS Account| StaffAccounts-Valid.csv
|1.2  Fail to Login with invalid FMS Account| StaffAccounts-Invalid.csv
|1.3 Fail to Login with valid Account but no master secret| *No Test Data required*
|1.4 Fail to access APIs without valid Token| UserToken-Invalid.csv (`lib\create-invalid-token.js` will help generate the invalid tokens)
|1.5 Fail to access upload file API without valid Token| UserToken-Invalid.csv

> *Other cases are not implemented yet!*

## Execution of Test Cases

1. Manually execution

    > Execute each collection in `Postman` with test data set.

    or

2. Automatic execution

    > Write a Node.js script with `newman` to run all the collections with corresponding test data sets.

## End of this readme
