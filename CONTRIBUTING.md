# Contribution Guide

This repo acts as a reference implementation of the Decentralized Web Node (DWN) specification. Before getting started, we highly recommend that you read the [DWN spec doc](https://identity.foundation/decentralized-web-node/spec/). The specification is still in a draft / incomplete state. Anything related to the general architecture, features, or bugs with respect to DWN in general are best addressed via issues and pull requests within the [spec repo](https://github.com/decentralized-identity/decentralized-web-node). During early development, we'll be working on the specification and implementation in parallel. If you're confused about where to post your question, bug, or feature request, don't sweat! Go ahead and post it in either repo and we'll go ahead and move it if need be.

The general process we hope to follow is:
- Submit a proposal as a PR in the DWN spec repo. 
- Iterate on the PR until it gets pulled into `main`. 
- Implement said proposal in this repo and submit a PR
- Iterate on PR until its ready for `main`

Given that we're still in early stages of development, this contribution guide will certainly change as we near a beta release. Until then, things will be a bit ragtag but there's still plenty of opportunities for contribution.

As we work our way towards a beta release, we'll be creating more focused issues with the following labels:
- `bug`
- `documentation`
- `good first issue`
- `help wanted`

These issues are excellent candidates for contribution and we'd be thrilled to get all the help we can get! You can take a look at all of the Issues that match the labels above [on the Issues tab](https://github.com/TBD54566975/dwn-sdk-js/issues?q=is%3Aopen+label%3A%22help+wanted%22%2C%22good+first+issue%22%2C%22documentation%22%2C%22bug%22+)

We suggest the following process when picking up one of these issues:
- Check to see if anyone is already working on the issue by looking to see if the issue has a `WIP` tag. 
- Fork the repo and create a branch named the issue number you're taking on
- Push that branch and create a draft PR
- paste a link to the draft PR in the issue you're tackling
- We'll add the `WIP` tag for you
- work away. Feel free to ask any/all questions that crop up along the way
- Switch the draft PR to "Ready for review"

## 🎉 Hacktoberfest 2024 🎉

`dwn-sdk-js` is a participating in Hacktoberfest 2024! We’re so excited for your contributions, and have created a wide variety of issues so that anyone can contribute. Whether you're a seasoned developer or a first-time open source contributor, there's something for everyone.

### Here's how you can get started:
1. Read the [code of conduct](https://github.com/TBD54566975/dwn-sdk-js/blob/main/CODE_OF_CONDUCT.mdd).
2. Choose a task from this project's Hacktoberfest issues in our [Project Hub](https://github.com/TBD54566975/dwn-sdk-js/issues/806). Each issue has the 🏷️ `hacktoberfest` label.
5. Comment ".take" on the corresponding issue to get assigned the task.
6. Fork the repository and create a new branch for your work.
7. Make your changes and submit a pull request.
8. Wait for review and address any feedback.

### 🏆 Leaderboard & Prizes
Be among the top 10 with the most points to snag custom swag just for you from our TBD shop! To earn your place in the leaderboard, we have created a points system that is explained below. As you complete tasks, you will automatically be granted a certain # of points.

#### Point System
| Weight | Points Awarded | Description |
|---------|-------------|-------------|
| 🐭 **Small** | 5 points | For smaller tasks that take limited time to complete and/or don't require any product knowledge. |
| 🐰 **Medium** | 10 points | For average tasks that take additional time to complete and/or require some product knowledge. |
| 🐂 **Large** | 15 points | For heavy tasks that takes lots of time to complete and/or possibly require deep product knowledge. |

#### Prizes
Top 10 contributors with the most points will be awarded TBD x Hacktoberfest 2024 swag. The Top 3 contributors will have special swag customized with your GitHub handle in a very limited design. (more info in our Discord)



### 👩‍ Need help?
Need help or have questions? Feel free to reach out by connecting with us in our [Discord community](https://discord.gg/tbd) to get direct help from our team in the `#hacktoberfest` project channel.

Happy contributing!

---

## Development
### Prerequisites

| Requirement | Tested Version | Installation Instructions |
| ----------- | -------------- | ------------------------- |
| `Node.js`   | `v18.17.0`     | There are many ways to install `Node.js`. Feel free to choose whichever approach you feel the most comfortable with. If you don't have a preferred installation method, you can visit the official [downloads](https://nodejs.org/en/download/) page and choose the the appropriate installer respective to your operating system |

### Running tests
* Running the `npm run test:node` command from the root of the project will run all tests using node. 
  * This is run via CI whenever a pull request is opened, or a commit is pushed to a branch that has an open PR.
* Running the `npm run test:browser` command from the root of the project will run the tests in browser environments.
  * Please make sure there are no failing tests before switching your PR to ready for review! This validation is automated when you open a new pull request.

### Developing and testing custom store implementations
Here is a guide on how to develop and test a custom implementation of the backend storage for DWN:

1. Implement one or a combination of the `DataStore`, `MessageStore`, and `EventLog` interfaces.
1. Import the `TestSuite` class for a new mocha test.
1. Invoke `TestSuite.runStoreDependentTests(...)` in `mocha`, this will run all store dependent tests.
1. Make sure that all store dependent tests pass.

> NOTE: currently the test suite is only exported in the ESM module.

Example code:
```ts
import { TestSuite } from '@tbd54566975/dwn-sdk-js/tests';
import { yourMessageStore, yourDataStore, yourEventLog } from 'your-custom-stores';

describe('Custom data store implementation', () => {
  TestSuite.runStoreDependentTests({
    messageStore: yourMessageStore,
    dataStore   : yourDataStore,
    eventLog    : yourEventLog,
  });
});
```

### Running benchmarks

Benchmarks should be run directly using `node` (e.g. `node benchmarks/store/index/search-index.js`).

Note that some benchmarks require that `npm run build` has been run beforehand.

Any dependencies needed by benchmarks should be in `devDependencies` (e.g. `index-store` for `node benchmarks/store/index/index-store.js`).

### Code Style
Our preferred code style has been codified into `eslint` rules. Feel free to take a look [at the relevant `.eslintrc` file](https://github.com/TBD54566975/dwn-sdk-js/blob/main/.eslintrc.cjs). Running `npm run lint` will auto-format as much as `eslint` can. Everything it wasn't able to will be printed out as errors or warnings. Please make sure to run `npm run lint` before switching your PR to ready for review! We hope to have this automated via a github action very soon.

### Code Guidelines
1. A `TODO` in comment must always link to a GitHub issue.

### Available NPM Commands
| command                           | description                                                                                                        |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| `npm run test:node`               | runs tests and type checking                                                                                       |
| `npm run test:node-grep`          | runs specific tests matching a pattern. Requires the -g option. For example: `npm run test:node-grep -g "RecordsReadHandler.handle"`                                                       |
| `npm run test:browser`            | runs tests against browser bundles in headless browser                                                             |
| `npm run test:browser-debug`      | runs tests against browser bundles in debug-ready Chrome                                                           |
| `npm run build`                   | transpiles `ts` -> `js` as `esm` and `cjs`, generates `esm` and `umd` bundles, and generates all type declarations |
| `npm run build:esm`               | transpiles ts -> js as `esm`                                                                                       |
| `npm run build:cjs`               | transpiles ts -> js as `cjs`                                                                                       |
| `npm run build:bundles`           | generates `esm` and `umd` bundles                                                                                  |
| `npm run build:declarations`      | generates all type declarations                                                                                    |
| `npm run clean`                   | deletes `dist` dir                                                                                                 |
| `npm run lint`                    | runs linter and displays all problems                                                                              |
| `npm run lint:fix`                | runs linter and attempts to auto-fix all problems                                                                  |
