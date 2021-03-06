# Overview
This repository contains a Restful service to handle the Fibonacci calculation. It also contains the unite test scripts, Jmeter test script for performance and function test, and other function test methods. About product management and maintain in 5 years, I think that a cloud product can live more than 3 years is a sales success and development success. So, we had to support marketing and development both to achieve it. I clarify this from five aspects: Marketing, Organization, System landscape, Continues delivery and Operation. And the system architecture diagram was desgined in section "System Architecture" <br>

[![Build Status](https://travis-ci.org/i070595/emc2.svg?branch=master)](https://travis-ci.org/i070595/emc2)

## Marketing
Provide stable and quality service will be our commitment to customer. The product’s market segment will be University, Research center and calculation service provider. To success setup an echo system is the key to achieve success. From development side, We will fully support and quickly response the requirements from Marketing<br>

## Organization
In order to quick response to market requirements for this small products, we'll adpot Rapid Iteration for our development. Based on the responsibility, we setup below teams to support marketing and development<br>
* **Customer support team:** Customers message and requirement.<br>
* **Development team:** Product bug fixing, new feature development, innovation and deployment interface.<br>
* **CD team:** Continues delivery system and testing center.<br>
* **DevOps team:** Online system monitor and operation, system deployment and upgrade.<br>

## System landscape
The product development will be considered as Continues delivery mode, and all Dev and QA will work on the same platform and focused on their professional area. Dev and QA will not consider about environment, infrastructure and deployment, they will only consider about development requirements and deployment interface.<br><br>
The product landscape will considered as Micro-service structure, packaged in Docker and deployed on Mesos.<br>



**Product Development**<br>

System development team will focus on the Fibonacci number service development and customer requirements. The system will be developed under TDD principle, all feature should be defined as testable. Unit test will cover every code layers, and all service must be stateless.<br>

* **Fibonacci service development**<br>
    Developer and QA focus on this area to continues improve service quality, optimize request response speed and system perforce. In order to adpot Micro-service and deployment, the deployment interface will be defined as a protocal for each component to discover resource and print logs<br>

* **Testing**<br>
    * **Unit testing:** Dev will provide Unit testing code once their class was finished.<br>
    * **Function testing:** QA can book environment from CD center and do function testing rely on test case, every function or feature   cutoff, the test case and testing should be finished.<br>
    * **Integration testing:** All QA should provide e2e test case and upload to Testlink which used to manage test case. <br>
    * **Regression testing:** it covered by automation test scripts. When the system grow up, no one can grantee the quality regression                         without automation testing. All QA will delivery test script on function and e2e scenario. Developers                             should delivery unit test case when their features were finished.<br>
    * **Performance testing:** it will be covered by performance testing tools, like Jmeter.<br>
    * **Deployment and upgrade testing:** deployment and upgrade is not part of development but it is integration the whole production                                      to success. Without pay attention to this part, even we pass in every testing phase, we may                                       have high probability to fail. I suggest to divide this part to two phase: binary deployment                                      and database data upgrade.<br>

* **Testing tools** <br>
    * Jmeter for backend service testing and performance testing. <br>
    * Selenium for front service testing.<br>
    * Unit test tools for unit testing.<br>
    * Python to meet daily testing tools requirement.<br>
    * Test case and test plan are managed by TestLink or JIRA and JIRA capture.
    * All automation testing script will run in the Testing Center, all the logs will be collected and analysis. The result will send   to    stakeholders.<br>

* **Infrastructure development**<br>
    Load balancer will set front of the product and used to dispatch customer requests. Fib service will packaged into Docker and deployed on Mesos. Database will use MariaDB cluster. SQL service is deployed in docker and the data stored in Glusterfs.<br>

    The tech used to  support core service development,  including service deployment, Database, Loadbalancer and Filesystem, will be included in this field.<br>

## Continuous Delivery
The CD team will considered about product continues integration and delivery. Dev/QA will pull from / push to git repository. Code review, validation and Security scan will automatically run in routine jobs on each branch. Once a code submit successfully, Build Server will automatically build a builder for Testing. The testing center will automatically deploy an environment to run sanity testing scripts. QA can also book an environment for manually testing, automation testing script development or performance testing. Once the code branch was freeze and testing passed in integration environment, the build will be tag as release candidate.<br>

## Operation
System operation team will focus on the online system monitor, in time action for online issues and collect online issues. They will use several tools to monitor the system and keep evidence for bug tracking. etc. ELK, Jiankongbao. When they started to deploy/upgrade the sytem, stakeholders will be notify to join the deploy/upgrade process<br>

## How to run
    pip install -r requirements.txt
    python manage.py runserver --host 127.0.0.1 --port 5000

## Other function testing
Use httpie run function testing <br>

    pip install httpie

Run in command<br> 

    http GET http://127.0.0.1:5000/api/v1.0/fib/10 
    http GET http://127.0.0.1:5000/api/v1.0/fib/100 
    http GET http://127.0.0.1:5000/api/v1.0/fib/0
    http GET http://127.0.0.1:5000/api/v1.0/fib/-0
    http GET http://127.0.0.1:5000/api/v1.0/fib/-1
    http GET http://127.0.0.1:5000/api/v1.0/fib/1asdfasdfasdfasdfasdfasdfsaf
    http GET http://127.0.0.1:5000/api/v1.0/fib/
    http GET http://127.0.0.1:5000/api/v1.0/fib/   
    http GET http://127.0.0.1:5000/api/v1.0/
    http GET http://127.0.0.1:5000/api/
    http GET http://127.0.0.1:5000/
    http GET http://127.0.0.1:5000/asdfasdf
    http GET http://127.0.0.1:5000/api/v1.0/fib/asdf 
    http GET http://127.0.0.1:5000/api/v1.0/fib/-10 
    http GET http://127.0.0.1:5000/api/v1.0/fib/$#@ 

Use Jmeter case run function testing <br>

    apt-get install jmeter

Run in command <br>

    jmeter -n -t <jmeter_test_script_path>

## System Architecture
Below is a draft architecture of FibService product environment architecture.<br>

![structure](https://github.com/i070595/picture/blob/master/structure.JPG)
