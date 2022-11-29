# File Storage

BOPTEST-Service depends on object-based storage for retaining user content such as test cases and test output. In a production environment this is intended to be Amazon S3, however [Minio](https://min.io) provides a S3 compaitable API, so in local development and even some production environments Minio is used. The purpose of this document is to define the organization of object keys used by BOPTEST-Service. S3 (and Minio's implementation of the S3 API) is not intrinsically hierarchical, however `/` characters used in key names are treated as delimiters by many of the S3 APIs, and BOPTEST-Service uses this delimiter for organizational purposes.

## Test case files

New test cases are added to BOPTEST-Service by uploading fmu files to object storage using the following naming convention as the key for each test case.
```
testcases/<user_id> | shared/<testcase_id>/<testcase_id>.fmu
```
User specific test cases are stored within the `testcases/<user_id>` prefix, while the formal BOPTEST test cases which are available to all BOPTEST users are stored under the `testcases/shared` prefix.

## Test results

When a test is completed, the entire working directory of the test is archived and storaged in object storage using the following key naming conventions.
```
simulated/<user_id> | <client_ip>/<test_id>.tar.gz
```
Each completed test is stored under the prefix `simulated/<user_id>` if the user is known, however if the user is anonymous then results will be stored under the key `simulated/<client_ip>` where `client_ip` is the IP address of the client which initiated the test.
