# Continuous Integration

Reference for this topic has been taken from the sixth chapter (Deployment) of Sam Newman's Building Microservices book

The core goal of CI is to keep everyone in sync with each other, which we achieve by making sure that newly checked-in code properly integrates with existing code.
To do this, a CI server like Travis or Jenkins  must be used to detect that the code has been committed, it should check out the code and carry out some verification like making sure the code compiles and that tests pass.

**Three Rules For CI:**

1) Frequent checkin to the repo's mainline branch:
If your repo's mainline is development or master, you have to make sure that your code integrates. If your code is not checked in frequently with others, then this makes future integration harder. Using feature branches are great, however, it is important to integrate as frequently as possible with the mainline branch.

2) Suite of tests to validate new code changes:
In order to ensure that the new code changes have not broken the behavior of the system, it is important to have tests that run against your code.

3) When the build is red, the top priority of the team is to fix the build.
A red build means the last change possibly did not integrate with the existing code. All further check-ins that are not related to fix the build must be stopped and the goal has to be to get the build passing again.

**Example Usage - Travis Configuration In Java**  
  Travis docs has a section for different programming languages. You can refer to that based on the language you are using - `https://docs.travis-ci.com/`

For Java apps using maven, in the `.travis.yml` file, if you have:

```
language: java
install:
- mvn clean package
```
If your repository is configured for Travis CI, it will build and run tests (if there are no settings in pom.xml to skip tests)

**Single Repo For Each Service And Corresponsing CI Build**  
  Every microservice SHOULD have its own independent source code repo and its corresponding CI build. The following configurations are discouraged:
  - having a single repo for multiple services with separate CI builds
  - having a single repo for multiple services and having one CI build for all the services
