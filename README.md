# Node API Template
Template project for setting up a Node project.
- [Template Node API](#node-api-template)
  - [Requirements](#requirements)
  - [Setting up a Node project](#setting-up-a-node-project)
  - [Development](#development)
    - [Libraries in use](#libraries-in-use)
    - [Workflow](#workflow)
    - [Testing](#testing)
    - [Static Analysis](#static-analysis)
    - [Project structure](#project-structure)
    - [CI/CD](#continuous-integration)
  - [Why I made this project](#why-i-made-this-project)
    - [Baseline](#baseline)
    - [Purpose](#purpose)
    - [Goals](#goals)
    - [Challenges](#challenges)

## Requirements
1. Node.js v16
2. SQLite (if used)
3. Redis (if used)
4. Any DB provider (MariaDB is my default)
5. Postman

## Setting up a Node project
My Node projects are managed using npm. Package requirements and dependencies are listed within package.json. Package-lock.json contains all dependencies listed with package.json but locked to specific versions to ensure compatibility.

Package.json has a scripts section where commands can be placed. See the sections [Commands](#commands) for more details

To set up the project, first make sure you have cloned the repository into its own directory.
Once done, in the terminal in the folder run `npm install` which will install all packages the project requires

## Development
### Libraries in use
My projects make use of all or some of the following libraries
- [better-sqlite3](https://www.npmjs.com/package/better-sqlite3) A synchronous API for use with sqlite3
- [sequelize](https://www.npmjs.com/package/sequelize) A ORM wrapper that supports multiple database dialects
- [node-gzip](https://www.npmjs.com/package/node-gzip) A compression wrapper
- [redis](https://www.npmjs.com/package/redis) Allows accessing redis locally or remote and performing actions on them
- [mocha](https://www.npmjs.com/package/mocha) Testing framework
- [chai](https://www.npmjs.com/package/chai) assertion library
- [chaiAsPromised](https://www.npmjs.com/package/chai-as-promised) a promise based extension for chai to allow easier testing of async functions
- [supertest](https://www.npmjs.com/package/supertest) HTTP mocking requests for testing
- [mariadb](https://www.npmjs.com/package/mariadb) for use with sequlize
- [axios](https://www.npmjs.com/package/axios) Making AJAX requests similar to fetch
- [nodemon](https://www.npmjs.com/package/nodemon) automatic recreation of the node server during development

**Better SQLite3:**
I use this as it is very simple to use, no callback hell and is much faster than the asynchronous on offer from node-sqlite3. No need to use async/await here.

**Sequelize:**
I use this as an ORM, abstracting away associations and allowing models and querying them to be performed much more efficiently than might be possible with raw SQL. AS well is the benefits of a bit more security. Supports lazy loading as well as eager loading

**Node Gzip:**
Promise based wrapper to compress responses to a gzip format. This is useful for reducing response times, from first to last byte for larger responses. 

**Redis:**
In memory key-value store, mainly used for caching. 

**Mocha:** 
The primary testing framework for my projects

**Chai:** 
Assertion library for use with mocha, offering both expect style and assert in testing

**Chai as Promised:**
A promise extension to chai to allow far easier testing of aync functions

**SuperTest:**
A mocking service for testing HTTP requests

**Mariadb:**
This is the primary database used for sequelize, and sequelize requires this package for working with the database

**Axios:** 
As fetch is not implemented in Node currently, this is for making AJAX requests

**Nodemon:**
For restarting the node server automatically when changes in the project are detected

### Workflow
1. For all functions written, write a test that tests both successful and failure, and anticipate edge cases
2. Single Action, if a function is creating and modifying a input, it should only be doing one of those.
3. Iterations:
    - Keep the original input clean, create a copy through maps or filters(etc) if you are changing something. Keep the input unmodified
    - use a foreach if you are creating output i.e logging or outputting
    - entries vs values vs keys: Know when to use them
    ```js
    let user = {
            name: "John",
            age: 30
        };

    Object.keys(user) = ["name", "age"]
    Object.values(user) = ["John", 30]
    Object.entries(user) = [ ["name","John"], ["age",30] ]
    ```
4. Returns:
    - if null/empty/undefined is a valid parameter for your function, do not throw an error, otherwise, throw an error so that
    try/catch blocks may be used to more easily find errors
    - Return as early as possible, so that code isn't executed needlessly
5. If using Regex, explain your regex so that others may understand it
6. Functions should be declared using consts. If you need to make use of specific parameters available to functions, use functions, as this keeps clashes
8. run `npm run lint` before committing to avoid simple CI failures

### Testing
### Static Analysis
### Project Structure
### Continuous Integration

## Why I Made this Project
### Baseline
### Purpose
### Goals
### Challenges
