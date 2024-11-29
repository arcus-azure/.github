# Contributing to Arcus
🎉 First off, thanks for taking the time to contribute! We're really glad you're reading this. 🎉

The following set of guidelines will help you in contributing to Arcus repositories.
But, no worries, if you forget something or have problems with some of these steps, we're happy to help! In those cases: create a PullRequest on the repository so we can talk about it.

This contribution guide has the following content:
- [Contributing to Arcus](#contributing-to-arcus)
  - [Issues and discussions](#issues-and-discussions)
  - [Pull Requests](#pull-requests)
    - [Forking](#forking)
    - [Implementing changes](#implementing-changes)
    - [Review and merge of the changes](#review-and-merge-of-the-changes)
  - [Project structure](#project-structure)
  - [Way of working](#way-of-working)
  - [Code guidelines](#code-guidelines)
    - [General](#general)
    - [Testing](#testing)
  - [Documentation](#documentation)
  - [THANK YOU you for your future contribution! ♥](#thank-you-you-for-your-future-contribution-)

## Issues and discussions
We are happy to discuss ideas and possible features or problems.

**In these cases, we would like you to create a discussion**
- You want to discuss a raw idea with us
- You have a question on the library, how to use it or where to find something
- You want to raise a concern

**In these cases, we would like you to create an issue**
- You encounter a problem or bug while using Arcus.
- You have a clear idea for a feature or enhancement in Arcus.

After you have created an issue, work will will be assigned by the code owners of the Arcus library.  However, you are also encouraged to fix the bug you've reported or implement the feature that you've proposed yourself as well!  In that case, it is recommended to check with the code owners of the Arcus repository first before diving into the code.


## Pull Requests
Changes to the code-base are always done via a pull request.
If you are facing a bug that is really bugging you, or if you're eagerly waiting for some feature to be implemented, you can take matters into your own hands and fix the bug or implement the feature yourself!

You can do this by **forking** the repository to your personal GitHub account and start working on the forked repository.  Once you've finished implementing the changes, create a pull request to the upstream Arcus repository to make your changes official!

### Forking
Make sure that you have forked the Arcus repository to which you want to contribute to your personal GitHub account. We work solely with pull requests (PRs) for new features or adaptations.

> More information on GitHub forking is available [here](https://guides.github.com/activities/forking/).

### Implementing changes
Once you've forked the repository, you can start making changes to the fork in your own GitHub account. When working on an issue, we recommend that you create a feature-branch on your own fork and make the changes on that feature branch. By doing that, you can keep your own `main` branch up to date with the current changes.

### Review and merge of the changes
When you're finished implementing the changes that are required for a feature or bug-fix, create a pull request for your feature branch into the `main` branch of the upstream Arcus repository.
Your pull request will be reviewed, and once an Arcus code owner has reviewed and approved the pull request, the changes will be merged into the Arcus repository.

## Project structure
All our Arcus projects are structured the same way.

- `src` folder with the actual code library
- `build` folder with the YAML build pipelines and templates for Azure DevOps
- `docs` folder with the current published and preview feature documentation
- `.github` folder with the governance information like: current issue and pullrequest templates 

## Way of working
Your assigned work should contain three things:
- The changes in the code base (new feature, fix, enhancement)
- The necessary unit/integration tests to verify the changes
- The update feature preview documentation so it can be included in the next release

These three things are items the code owners will verify when you submit a Pull Request.

## Code guidelines
We have some code style guidelines but don't be overwhelmed by this. We'll help you during the review of your PullRequest.

### General
- Every public field/method should be documented with XML docs (summary, params, exceptions)
- Every async method should be suffixed with `Async`
- One file should only contain one class
- Variable names should have a clear name and abbreviations should be avoided
  - Exceptions are LINQ statements, for loops, etc
- Private class fields should be prefixed with `_` such as `_serviceBusClient`
- Avoid using optional parameters for constructors and public methods
- If-statements that use a one-liner should be wrapped in `{ }`, an exception could be a return statement or an exception
- Avoid doing inline method calls to improve readability
  - Example to avoid - `throw new ApplicationException($"Event grid publishing failed. Content {await response.Content.ReadAsStringAsync()}");`

It's ok to use `var` when the type of the variable is clear, but when calling methods you should explicitly mention the expected type.

Example:
```csharp
// OK
var value = "some value";
// OK
string value = "some value";
// NOK
var value = GetValue();
```

### Testing
All the tests are located in the `Tests` solution folder of the Arcus library. All public functionality should be thoroughly tested with unit tests. These tests are always in the `Arcus.<library>.Tests.Unit` project. More advanced scenarios and the full workings of a feature are checked with integration tests and are always in the `Arcus.<library>.Tests.Integration` project.

- A test should only test one specific scenario and one specific flow (ie. happy or failure)
- All tests for one class should be consolidated into one test class
  - Example `SecretKeyHandlerTests` contains all tests for the `SecretKeyHandler` class
- Every test method should have the following naming convention `{Method To Test}_{Scenario}_{Expected Outcome}`
  - Example: `Validate_WithValidSecretName_ShouldPass`

Integration tests will usually require an `appsettings.private.json` or `appsettings.local.json` where the secret information for the tests will be inserted.
For local development, you should create your own appsettings file and fill in these secrets. The file will be ignored when pushing your changes so no secrets are made public.

## Documentation
All the available feature documentation is located under the `docs` folder. If your feature has impact on public functionality, you'll have to change the feature documentation too.
This will be done in the `./docs/preview` folder of the Arcus library. There you'll find a functional split of the functionality in markdown (`.md`) files.

Normally, you should quickly find which file you should change for an enhancement or fix.
For new features, please make sure that you keep the same structure of documentation features:

````
---
title: "Your feature description"
layout: default
---

# Your feature description
Short summary of what this Arcus feature provides.

## Your detailed functionality
More in-depth description of what the feature does.

```csharp
YourModel test = YourMethod(); 
```
````

___
## THANK YOU you for your future contribution! ♥
