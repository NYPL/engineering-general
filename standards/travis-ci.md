# Travis CI #

## What does Travis CI/CD do? ##

### CI: Continuous Integration ###

In software engineering, continuous integration (CI) is the practice of merging all developer working copies to a shared mainline several times a day. (from Wikipedia)

### CD: Continuous Deployment ###

Continuous deployment is a strategy for software releases wherein any code commit that passes the automated testing phase is automatically released into the production environment, making changes that are visible to the software's users.

## Process ##

In NYPL Digital's CI/CD stack, when a pull request is merging with, e.g., `development` branch, a series of steps is taken to build, test, and deploy to the branch.  

**Travis CI** is a tool with options to deploy to our services of choice, e.g. AWS Elastic Beanstalk.

The series of steps used to build, test, and deploy are stored in the configuration file `.travis.yml`. The file is usually located at the root level of each code repository.

### .travis.yml ###


## Possible trouble spots

### Chrome
When using Chrome to conduct tests such as with `karma`, Chrome is not installed by default on the virtualization environment.

## References ##
* [Travis CI: Core Concepts for Beginners](https://docs.travis-ci.com/user/for-beginners/)
* [Travis CI: Customizing the Build](https://docs.travis-ci.com/user/customizing-the-build/)
