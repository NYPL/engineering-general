# Preferred Technologies

The Digital department at NYPL was formed from several different teams, that had generally been independent and did not share standards on technology, etc. This means that the systems that Digital is responsible for use many different languages, frameworks, deployment environments etc., etc.

This can naturally lead to some issues, as not everyone can be conversant in every technology that is used (while this problem is certainly not unique to NYPL it is particularly pronounced here). This in turn can lead to resource constraints in planning, as you don't just need to worry about what team should deal with something, you also need to consider the individual skillsets. Additionally it can also cause problems when creating new services — should we use Rails, node, Python, Java, PHP? Microservice or monolith? 

Therefore, to help inform any technology decisions in the future we have the following guiding principles:

* Except in particular, specialist areas (mobile development, SimplyE) new development should use JavaScript or Ruby.
* If you wish to use a different language, you should discuss with Engineering Managers first, and have considered how the thing you are developing will be maintained in future.
* Within those languages, our standard framework/libraries are Rails, node, Express, React [any others?]
* We like microservice architectures, which should use RESTful APIs and/or event streams or message queues (the wide variety of languages and frameworks we use make microservices more attractive, as we are less constrained by prior use of languages than we would be in a monolithic application, and, at worst, it is easier to rewrite a microservice in a different language than a larger app).
* We prefer our RESTful APIs to use JSON as the main data exchange format
* All APIs we create should have Swagger Docs endpoints
* Our preferred deployment platform is AWS
* For traditional server apps, we prefer to develop and deploy them as Docker containers [more details in separate doc to come]
* APIs could be implemented as Docker containers, or as Lambdas, as appropriate (appropriateness up for discussion!)
* For event-driven architectures we tend to use AWS lambdas and kinesis event streams.
* As well as event streams, we also like message queues where appropriate. 
* As a rule of thumb — events should be used when there is a replayable sequence of events; queues should be used for tracking and managing tasks. E.g., an update of a record is an event; propagating an update into different repositories could be managed as a task in a queue.
* Any particular lambda should either be invoked by messages or by API endpoints, not both
* Any new repos should be created in the github.com/NYPL 
* We like to use CI/CD to automatically test and deploy our new code, and Travis is our preferred tool for CI/CD. 
* Whenever working on a codebase that does not have CI/CD we should make time (and create tickets) to get it set up




