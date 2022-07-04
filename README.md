# Engineering Onboarding Guide

Hey there! You're probably reading this because you've been invited to take one of our code challenges or are working on an engineering project. Welcome!

Code quality is very important to us, and we hope it is to you too. In this guide we'll share our engineering process that we use to ensure that we can build quickly while keeping our projects stable and maintainable. We'll cover topics like code style, commit guidelines, project workflow, and team communication.

## Code Style

Some developers feel the need to debate code style. Other engineers will use the project's style and get stuff done. We prefer engineers who get stuff done. Consistency is important, please follow these guidelines.

We use the [JavaScript Standard Style](https://standardjs.com/) in our code. This is the style used by npm, GitHub, Zeit, MongoDB, Express, Electron, and many others. Be sure to use an automatic formatter like [standard-formatter](https://atom.io/packages/standard-formatter) for Atom and [vscode-standardjs](https://marketplace.visualstudio.com/items/chenxsan.vscode-standardjs) for Visual Studio Code.

Line length should be limited to 80 characters.

## Code Principles

* Code should be as simple, explicit, and as easy to understand as possible.
* Functional style is preferred to OOP. When possible functions should be pure and not rely on shared state or side effects.
* Avoid large frameworks; use small modules that are easy to understand.
* Modules must use this order so that they can be understood quickly when skimmed:
  1. External dependencies: anything listed in `package.json`, e.g. `require('http')`
  2. Internal dependencies: any files created in the project itself, e.g. `require('./api')`
  3. Constants and other setup: this includes anything *absolutely necessary* to be defined before `module.exports`
  4. Exports: `module.exports` should be as close to the beginning of the file as possible. The module should export either a single function or a "catalog object", e.g. `module.exports = { method1, method2, ... }`
  5. Functions: these go after the above sections. Use function hoisting to control the placement of your functions so that important, high-level functions are above smaller more-general utility functions.
* Use descriptive variable names. Function names should be a verb like `route()` or verb combined with a noun like `routeRequest()`.
* Keep your functions short. If your function is over 40 lines, you should have a good reason.
* Functions should not accept more than 3 arguments. Use a single options object if you need more arguments.
* Keep nesting to a minimum. Use [early returns](https://blog.timoxley.com/post/47041269194/avoid-else-return-early), single-line conditionals, and function calls.

## Git & Github

Version control is a project's best source of documentation when done correctly. When trying to understand code it's extremely useful to use `git blame` to find both the PR and the issue associated with that change.

PRs should be small and focused. Each commit should solve a single problem and be covered by a test that exemplifies that particular feature or fix.

All PRs must be reviewed by a teammate before they are eligle to be merged into  the `master` branch. Large PRs are difficult to review. Be sure to break large PRs into smaller ones so that they can be reviewed quickly and deployed to production.

* Never commit passwords, access tokens, or other credentials into version control. If you think you absolutely have to, ask first. If you do this by accident, tell someone immediately.
* Each commit should be as small and as simple as possible.
* The project must be operational and have all tests passing after every commit.
* Use [Conventional Commits](https://www.conventionalcommits.org)
  * See the "Commit Types" section below
  * Valid types are `chore:`, `docs:`, `style:`, `refactor:`, `perf:`, and `test:`
* Do not mix feature changes (added functionality) with fixes (restored functionality), refactors (no change in functionality), or style changes (only whitespace or other cosmetic changes).
* Before a PR is ready for review, make sure that it is a single commit. If the combined commit is too large or disparate, consider multiple PRs.
* The exception to the above single commit rule is when a PR introduces new packages. Create one extra commit in the same PR for each new package your PR needs.
* Do not modify a project's `.gitignore` to add files related to your editor or environment. Use your own [global .gitignore](https://stackoverflow.com/questions/7335420/global-git-ignore/22885996#22885996) for that instead.
* Be sure that your PRs have descriptive titles that explain what has been changed. Typically the commit message is sufficient. "Fixes #66" is not.
* When submitting a PR with UI or visual changes, please add before and after screenshots to the PR. This makes it easy for the reviewer to quickly see what has been done.
* If a change has been requested on your PR, subsequent commits should be squashed into the original using `git rebase -i HEAD~n`. When pushing to remote, you can use `git force --push`.

## Commit Types

Commit types (e.g. `feat`, `fix`, `refactor`, `style`) are important because they are a signal to the reviewer for what they should be looking for and how much scrutiny the review needs. Reference from [Angular](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines):

- feat: A new feature
- fix: A bug fix
- refactor: A code change that neither fixes a bug nor adds a feature
- style: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
- test: Adding missing tests or correcting existing tests
- docs: Documentation only changes
- perf: A code change that improves performance
- build: Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)
- ci: Changes to our CI configuration files and scripts (example scopes: Travis, Circle, BrowserStack, SauceLabs)

### Descending Levels of Scrutiny and Test Requirements

**Feature** commits require the most scrutiny. They add or change functionality, require additional tests, and have the greatest chance of introducing a bug.

**Fix** commits are smaller and have a more bounded scope than feature commits. Features usually introduce multiple new behaviors, but fix commits will only modify a single behavior. Fix commits need to provide additional test coverage because the existing tests were insufficient to catch the error. Feature commits should have multiple tests for these behaviors, but fix commits typically introduce a single test to prove that the error has been fixed (test should fail without the fix inactive and pass with it active). These commits can introduce additional bugs, but it’s less common than feature commits.

**Refactors** need less scrutiny than feature or fix commits because little about the app changes. All consumers of the refactored part of the app should be 100% unaware of the change. If module A is refactored, and module B depends on A, module B does not need to be tested because A hasn’t changed anything from their perspective. Similarly, anything that depends on B doesn’t need to be tested either, no change should bubble up to cause issues. Since nothing is changing, any existing tests/QA should already be sufficient to catch any issues created by the refactor. If there are no tests for the code being refactored, there should be new tests included in the PR along with the refactor. If there are existing tests, the refactor should not generate additional tests.

**Style** commits need the least amount of scrutiny. They tend to be very repetive (converting from snake_case to camelCase, standardizing indentation, or changing newlines). These changes will have no functional impact on the code and any existing tests should be sufficient.

## Workflow

We use GitHub to manage our workflow. Each task is represented by an issue. Be sure to connect any PR you are working on to the appropriate issue, [following the instructions from GitHub on how to do so](https://help.github.com/en/github/managing-your-work-on-github/linking-a-pull-request-to-an-issue).


## Starting A New Project

Make sure to cover everything in the following sections when you are starting a new project & reference this section by creating a discussion thread when starting new projects.

- Read available documentation
- Set up the repository / codebase locally with database and environment variables
- Use the whole product from a user’s perspective and understand its features
- Look into the test cases for the features, as they can be a great source of documentation
- For back-end repositories make calls to their APIs understanding request & response structure
- For front-end repositories run the corresponding back-end repositories & find out the features by how - they interact with one another
- Create a Data-Flow-Diagram of the application of your understanding of the system and discuss with other team members
- If there are still some parts of them system that you do not understand, focus on what is known rather than what is unknown & check the names of the developers who has worked on that part of the system.
- Check and ask clarifying questions:
  - Check if you have required permissions in order to accomplish what is being requested.
  - Check if you have everything required in order to perform the task and ask about what you're missing / you'll need.
  - Check if you have all test environments, production environments. in case of having no access to test environments ask if it's okay to post to production in case of debugging any issue.
  - In case of the project not having any repository within the organization, check the following list:
    - Does the request needs to have a repository set up right now or can we create one later after completing some of the current tasks at hand? pick up an accurate name for the repository and ask for it to be set up with proper organizational access.
    - Does it need Dev Ops to be set up right now or can we set it up later without stalling the current progress? if requests are small, let everyone know you are making the changes in the production and ask for the Dev Ops to be created later without stalling progress.
- Create discussion threads and ask specific questions with [code references](https://docs.github.com/en/repositories/working-with-files/using-files/getting-permanent-links-to-files) & questions should include specific contexts in order:
  - Problem
  - Why it’s a problem
  - What you’ve done to attempt to solve it
  - What you think could solve it
  - What you are asking to do
