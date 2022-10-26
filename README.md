
# BOPTEST-Service

This software reformulates [BOPTEST](https://github.com/ibpsa/project1-boptest) into a web based software as a service architecture, which enables BOPTEST to support multiple clients and multiple simultaneous tests at a large scale. This is a containerized architecture that can be deployed on a personal computer, but is especially designed for deployment on commercial cloud computing environments such as AWS. For details about the BOPTEST project, refer to the project [homepage](https://boptest.net).

The canonical BOPTEST source code is incorporated into this repository as a git subtree located at `<project-root>/boptest` and used under the terms of the license located at `<project-root>/boptest/license.md`. 

A deployment of `BOPTEST-Service` is available at https://api.boptest.net

# Getting Started as a User

# Building and Running on a Personal Computer
1) Download this repository: clone this repo to your preferred location with 

 * ``git clone https://github.com/NREL/boptest-service.git preferred_location`` 
 
  where preferred_location is where you want to clone the repo to. 
  
2) Install [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/).

3) To build, use the following command within the root directory of the extracted software:

  * ``docker-compose up web worker provision``

4) In a separate process, use the test case API defined below to interact with the test case using your test controller.  Alternatively, view and run an example test controller as [described below](https://github.com/NREL/boptest-service#running-tests).
5) Shutdown the test case by the command ``docker-compose down`` executed in the root directory of this repository.
# Running Tests

Testing is based on the BOPTEST [test suite](https://github.com/NREL/boptest-service/tree/develop/boptest/testing) with small adaptations to conform to the BOPTEST-Service API. Follow the [README](https://github.com/NREL/boptest-service/blob/develop/boptest/testing/README.md) for more information.

# Kubernetes Based Deployment

NREL maintains a helm chart for Kubernetes based deployments of BOPTEST-Service.

