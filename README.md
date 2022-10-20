# BOPTEST-Service

This software reformulates [BOPTEST](https://github.com/ibpsa/project1-boptest) into a web based software as a service architecture, which enables BOPTEST to support multiple clients and multiple simultaneous tests at a large scale. This is a containerized architecture that can be deployed on a personal computer, but is especially designed for deployment on commercial cloud computing environments such as AWS. For details about the BOPTEST project, refer to the project [homepage](https://boptest.net).

The canonical BOPTEST source code is incorporated into this repository as a git subtree located at `<project-root>/boptest` and used under the terms of the license located at `<project-root>/boptest/license.md`. 

A deployment of `BOPTEST-Service` is available at https://api.boptest.net

# Getting Started as a User

# Building and Running on a Personal Computer

# Running Tests

Testing is based on the BOPTEST [test suite](https://github.com/NREL/boptest-service/tree/develop/boptest/testing) with small adaptations to conform to the BOPTEST-Service API. Follow the [README](https://github.com/NREL/boptest-service/blob/develop/boptest/testing/README.md) for more information.

# Kubernetes Based Deployment

NREL maintains a helm chart for Kubernetes based deployments of BOPTEST-Service.
