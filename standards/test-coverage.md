# Test Coverage

Apps SHOULD enforce a sane testing strategy. Some basic guidelines follow. Developers are encouraged to add and expand on this list. 

## Unit Testing

Unit test coverage SHOULD cover at least 70% of the codebase. 

If test coverage remains under 70%, each subsequent pull requests MUST at least nominally increase the overall coverage. 

Each unit test MUST test one and only one thing -- be clear and concise in your tests, and ALWAYS write tests that are independent of your other tests. 

Unit tests SHOULD NOT rely on external services. 

Unit tests SHOULD be able to be run repeatedly and produce the same results. 

Unit tests SHOULD be written before the implementation required to make them pass. 

Unit tests SHOULD aim to cover the import and custom logical choices in your code. They SHOULD be thorough -- beyond the code coverage percentage, it is important to cover ALL potential ways in which your code can function. 

Developers MUST document how to install all test dependencies and fully run their tests in their code repository's wiki or in their README. 

## Integration Testing

Where external services or applications are involved in your code, you MUST develop a plan for integration testing -- whether through automation or a logical series of manual steps. 

The method for integration testing SHOULD be described and documented in your code repository wiki. 

