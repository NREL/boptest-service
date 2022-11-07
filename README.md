


# BOPTEST-Service

This software reformulates [BOPTEST](https://github.com/ibpsa/project1-boptest) into a web based software as a service architecture, which enables BOPTEST to support multiple clients and multiple simultaneous tests at a large scale. This is a containerized architecture that can be deployed on a personal computer, but is especially designed for deployment on commercial cloud computing environments such as AWS. For details about the BOPTEST project, refer to the project [homepage](https://boptest.net).

The canonical BOPTEST source code is incorporated into this repository as a git subtree located at `<project-root>/boptest` and used under the terms of the license located at `<project-root>/boptest/license.md`. 

A deployment of `BOPTEST-Service` is available at https://api.boptest.net

# Getting Started

Clicking [this link](https://github.com/NREL/boptest-service/blob/documentation_readme_changes/docs/Introduction_to_BOPTEST_Service_APIs.ipynb) will take you to an interactive tutorial that will help you get familiar with both core BOPTEST APIs and BOPTEST-service APIs. Have fun! 

# BOPTEST-Service Specific APIs
## APIs for the regular user 

| Interaction                                                           | Request                                                   |
|-----------------------------------------------------------------------|-----------------------------------------------------------|
| List available test cases.                                |  GET `testcases` |
| Check if specific test case is in list of available test cases. Returns status code of `200` (OK) if found, `404` if not found.                                 |  GET `testcases/{testcase_name}` |
| Select a test case and begin a new test. A unique ``testid`` will be returned.                                |  POST ``testcases/{testcase_name}/select`` |
| Stop a running test.                                                   |  PUT ``stop/{testid}`` |

## APIs for admin users

| Interaction                                                           | Request                                                   |
|-----------------------------------------------------------------------|-----------------------------------------------------------|
| Get form data for the submitting BOPTEST test cases.                                |  GET ``/testcases/{testcase_name}/post-form`` |
| Delete a test case.                                |  DELETE ``/testcases/{testcase_name}`` |



# Building and Running on a Personal Computer
1) Download this repository: clone this repo to your preferred location with 

 * ``git clone https://github.com/NREL/boptest-service.git {preferred_location}`` 
 
  where `{preferred_location}` is where you want to clone the repo to. 
  
2) Install [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/).

3) To build, use the following command within the root directory of the extracted software:

  * ``docker-compose up web worker provision``

4) In a separate process, use the core [BOPTEST APIs](https://github.com/ibpsa/project1-boptest/tree/boptest-service#test-case-restful-api) as well as [BOPTEST-service APIs](https://github.com/NREL/boptest-service/tree/documentation_readme_changes#boptest-service-specific-apis) to interact with the test case using your test controller.  
Alternatively, view and run an example test controller as [described below](https://github.com/NREL/boptest-service#running-tests).
5) Shutdown the test case by the command ``docker-compose down`` executed in the root directory of this repository.


# Running Tests

Testing is based on the BOPTEST [test suite](https://github.com/NREL/boptest-service/tree/develop/boptest/testing) with small adaptations to conform to the BOPTEST-Service API. Follow the [README](https://github.com/NREL/boptest-service/blob/develop/boptest/testing/README.md) for more information.

# Kubernetes Based Deployment

NREL maintains a helm chart for Kubernetes based deployments of BOPTEST-Service.

