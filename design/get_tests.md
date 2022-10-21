# Add API to get all tests

## Overview

### Status: Design phase
This task attempts to add an API that returns the tests that are currently alive for a particular user. 

## Context

### Goal
Provide API to get which tests are currently being run by BOPTEST for that user. 

### Problem
1. For BOPTEST use cases like MegaBOP which are under development, bugs within MegaBOP could cause the user to lose the test_id. If the test_id is lost, there is currently no way to get the test-id again, and the user cannot interact with or stop a test anymore. The test_id is also a uuid which is hard to remember without noting it down somewhere. 
2. This task will eventually also help with designing and implementing a "kill test" API, which can remove a test that is stuck in a simulation loop. These tests don't respond to `stop` API calls. These hung tests will clog up workers and prevent the users from further using the BOPTEST API. 

## Design

### Software design

#### Sample API call: 

GET `BOPTEST_URL/tests?key=API_KEY`
or
GET `BOPTEST_URL/API_KEY/tests`

#### Psuedocode:

    When select call:
    	Add returned test_id to api_key:tests data structure
    	
    If test_id is not alive:
    or
    When test is done (how to know?):
    or
    If test fails or is killed:
    	Remove test_id from api_key:tests data structure 
	


### Redis storage (data structure) details
#### Alternative 1:
Use sets, with test_id as members. 

Advantages:
1. Unique elements
2. Less memory compared to hashes
3. Easy and simple implementation

####  Alternative 2:
Use hashes, with the test_id as keys, and put in the `model` as value. This will help identify the test_id. 

Advantages:
1. Unique keys
2. Easy to identify which model is being tested. Ability to add more info, if we need to.
3. Can carry over from old code  


## Additional Tasks

