# OpenAPI Contract Testing Tools



* [Schemathesis (github)](https://github.com/schemathesis/schemathesis)
    * [Introduction — Schemathesis 3.17.5 documentation](https://schemathesis.readthedocs.io/en/stable/introduction.html)
    * **PROS:**
        * Has CLI tool, or can also leverage python
        * 1600 stars on github
        * Reporting
            * If using only CLI tool, reporting drives you to online dashboard, and >1 API will require license/cost
                * Can do junit-style report, but not great
            * If using python lib, can use allure or anything that piggybacks off pytest reports
        * Can add state machine via hypothesis to manage request states
            * Need to add “links” to openapi spec  [https://schemathesis.readthedocs.io/en/stable/stateful.html#how-to-provide-initial-data-for-test-scenarios](https://schemathesis.readthedocs.io/en/stable/stateful.html#how-to-provide-initial-data-for-test-scenarios)
    * **CONS:**
        * Slow to run, even slower to run negative tests
        * Must license to use CI?
* ~~[https://github.com/MarketSquare/robotframework-openapidriver](https://github.com/MarketSquare/robotframework-openapidriver)~~
    * ~~?? product supported by single dev - having LOTS of problems getting it working - the LSP is just broken~~
    * ~~Only 17 stars and 2+ years old~~
    * ~~Already found 2 bugs that maintainer had to fix and BARELY got it running…no go~~
* ~~[Dredd(github)](https://github.com/apiaryio/dredd)~~
    * **~~PROS~~**
    * **~~CONS~~**
        * ~~Only experimental support for OAI 3.0 specs…~~
* [Postman/Portman](https://github.com/apideck-libraries/portman) *****TOP CHOICE*****
    * [Automating API Testing with Portman, Postman and Newman | by Tyler Owen | ITNEXT](https://itnext.io/automating-api-testing-with-portman-postman-and-newman-ec1a869cbc99) 
    * **PROS**
        * Reads openapi spec and creates postman collections with tests, and runs in newman
        * Can open/run the generated collection in Postman, aiding in debugging and test creation
        * Can add variation tests
        * Can easily add any/all requests/tests to postman collection
            * Probably do a separate collection for manually-created functional tests, but TBD
        * Executes very quickly
        * Can add stateful tests easily
        * Easily integrates w/ Jenkins thru [newman](https://learning.postman.com/docs/running-collections/using-newman-cli/command-line-integration-with-newman/#:~:text=Newman%20is%20a%20command%2Dline,CI)%20servers%20and%20build%20systems.)
    * **CONS**
        * Dependence on postman/newman (not a big con, just an external dependence)
        * No ability to write custom code, but appears to be totally customizable through the configs (see [repo example](https://github.ia.local/chrishyde/customermeta-portmanApi/blob/main/resources/portman-config.json) and [docs](https://github.com/apideck-libraries/portman#portman-settings))
* ~~[OpenAPI Mocking and Testing | Microcks.io](https://microcks.io/documentation/using/openapi/) ~~
    * **~~PROS~~**
        * ~~Imports/maps endpoints using OAI spec~~
        * ~~Supports non-REST protocols~~
            * ~~[https://microcks.io/documentation/using/tests/#event-based-apis](https://microcks.io/documentation/using/tests/#event-based-apis) ~~
        * ~~Nice dockerized solution with UI for everything, looks very OpenAPI-like and has a spec visualizer~~
    * **~~CONS~~**
        * ~~In order to produce working mocks, Microcks will need complete request/response samples in the OAI spec~~
            * ~~[https://microcks.io/documentation/using/openapi/#conventions](https://microcks.io/documentation/using/openapi/#conventions) ~~
            * ~~Sample spec:  [https://github.com/microcks/microcks/blob/master/webapp/src/test/resources/io/github/microcks/util/openapi/cars-openapi.yaml](https://github.com/microcks/microcks/blob/master/webapp/src/test/resources/io/github/microcks/util/openapi/cars-openapi.yaml) ~~
        * ~~Does not auto-gen based on the spec alone~~
        * ~~Very immature product~~
        * ~~UI-based test development~~
        * ~~No debugging ability~~
* ~~[https://docs.pact.io/](https://docs.pact.io/)~~
    * ~~Does not ingest openapi spec~~
    * ~~Contracts must be maintained on both consumer and producer side~~
* ~~[https://github.com/allenheltondev/postman-contract-test-generator](https://github.com/allenheltondev/postman-contract-test-generator)~~
    * ~~Natively uses postman api ($$) and product supported by single dev~~
* ~~[Jetbrains Aqua test automation IDE ](https://www.jetbrains.com/aqua/)~~
    * ~~Inbuilt openapi support~~
    * ~~Too immature~~
* ~~[Pactflow](https://pactflow.io/) ~~
    * ~~Uses pact.io~~
* ~~[API Testing | Sauce Labs Documentation](https://docs.saucelabs.com/api-testing/) ~~
    * ~~UI is clunky - can’t mass-modify or delete imported HTTP requests from OAI spec~~
    * ~~Latency way too high - one test takes way too long to run (377ms)~~
    * ~~Very clunky to import OAI spec and then have to manually "generate a test"~~
    * ~~All test mods must be done in UI~~


## CONSIDERATIONS:



* Language - Python, or language-agnostic/CLI tool
* Ingest OpenAPI spec and autogen tests
    * Contract tests
    * Stateful tests - data combinations, not just serially hitting endpoints with independent payloads
* Negative testing
* Fuzz testing
* Performance/load/spike(+/-) testing
    * Possibly a different tool/framework altogether
* Support for event-driven messaging services
* Paid vs. open-source
    * Prefer O-S as free, and more control over the tool
* Flexibility - licensing model (if paid)
* CI
    * Jenkins pipelines (plugins)
* Reporting
    * Allure
        * Tool to create a single HTML openable without allure server: [allure-single-html-file](https://github.com/MihanEntalpo/allure-single-html-file)
        * Allure as a docker container: [allure-docker-service](https://github.com/fescobar/allure-docker-service#customize-emailable-report)
    * Pytest
    * Html
        * HTMLExtra
            * [Newman reporter](https://www.npmjs.com/package/newman-reporter-htmlextra)
    * ?
* Eventually have a test-only DB or DBs for specific usage
    * Contract
    * functional/state
    * Perf/load/spike/etc.
    * etc..
