# Travis CI #

## What does Travis CI do? ##

### CI: Continuous Integration ###

From Travis CI documentation

> Continuous Integration is the practice of merging in small code changes frequently - rather than merging in a large change at the end of a development cycle. The goal is to build healthier software by developing and testing in smaller increments.

## Process ##

In NYPL Digital's CI/CD stack, when a pull request is merging with, e.g., `development` branch, a series of steps is taken to build, test, and deploy to the branch.  

**Travis CI** is a tool with options to deploy to our services of choice, e.g. AWS Elastic Beanstalk.

### .travis.yml ###

A series of steps used to build, test, and deploy are stored in the configuration file `.travis.yml`. The file MUST be located at the **root level** of each code repository, such as `NYPL/staff-picks/.travis.yml`. The file MUST be named `.travis.yml`, with a leading period in the file name.

### Build ###

A basic build on Travis CI consists of the following steps
1. `install`: installs required dependencies for the application
2. `script`: runs the build script(s) for the application

There are many steps in between that can be added for further customization. Here's a list of frequently used build stages on NYPL applications, from top to bottom of `.travis.yml` file:

1. `language`: Programming language of the code repository
2. Language version such as `rvm`, `node_js`, etc.

### Test ###

### Deploy ###

## Possible trouble spots

### Chrome
When using Chrome to conduct tests such as with `karma`, Chrome is not installed by default on the virtualization environment.

## References ##
* [Travis CI: Core Concepts for Beginners](https://docs.travis-ci.com/user/for-beginners/)
* [Travis CI: Customizing the Build](https://docs.travis-ci.com/user/customizing-the-build/)
