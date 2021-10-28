# Contributig to Arcus
🎉 First off, thanks for taking the time to contribute! We're really glad you're reading this. 🎉

The following set of guidelines will help you in contributing to  Arcus repositories.
But, no worries, if you forget something or have problems with some of these steps, we're happy to help! In those cases: create a PullRequest on the repository so we can talk about it.

This contribution guide has the following contents:

## Issues and discussions
We are happy to discuss ideas and possible features or problems.

In these cases, we would like you to create an issue:
- You encouter a problem or bug while using the Arcus library.
- You have a clear idea for a feature or enhancement in the library.

In these cases, we should like you to create a discussion:
- You want to discuss an raw idea with us
- You have a question on the library, how to use it or where to find something

Work will be assigned by the code owners of the Arcus library and it is recommended to check with them first diving into code.

## Forking
Make sure that you have forked the Arcus repository to which you want to contribute to your personal GitHub workplace. We work solely with pull requests (PRs) for new features or adaptations.

> More information on GitHub forking is available [here](https://guides.github.com/activities/forking/).

When working on an issue, we recommand that you create a feature branch on your own GitHub workplace and merge it via PullRequest into the `master` branch of the destination Arcus repository.
That way, you can keep your own `master` branch up to date with the current changes.

## Project structure
All our Arcus projects are structured the same way.

- `src` folder with the actual code library
- `build` folder with the YAML build pipelines and templates
- `docs` folder with the current published and preview feature documentation

## Way of working
Your assigned work should contain three things:
- The changes in the code base (new feature, fix, enhancement)
- The necessary unit/integration tests to verify the changes
- The update feature preview documentation so it can be included in the next release

These three things are items the code owners will verify when you submit a PullRequest.

## Code guidelines
We have some code style guidelines but don't be overwhelmed by this. We'll help you during the review of your PullRequest.

### General
- Every public field/method should be documented with XML docs (summary, params, exceptions)
- Every async method should be suffixed with `Async`
- One file should only contain one class
- Variable names should have a clear name and abbreviations should be avoided
  - Exception would be LINQ statements, for loops, etc
- Private class fields should be prefixed with `_` such as `_serviceBusClient`
- Avoid using optional parameters for constructors and public methods
- If-statements that use a one-liner should be wrapped in `{ }`, an exception could be return statement or exception
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
The all tests are located in the `Tests` solution folder of the Arcus library. All public functionality should be thoroughly tested with unit tests. These tests are always in the `Arcus.<library>.Tests.Unit` project. More advanced scenario's and the fully workings of the features are checked with integration tests and are always in the `Arcus.<library>.Tests.Integration` project. 

- A test should only test one specific scenario and a specific flow (ie. happy or failure)
- All tests for one class should be consolidated into one test class
  - Example `SecretKeyHandlerTests` contains all tests for the `SecretKeyHandler` class
- Every test method should have the following naming convention `{Method To Test}_{Scenario}_{Expected Outcome}`
  - Example: `Validate_WithValidSecretName_ShouldPass`

Integration tests will usually require an `appsettings.private.json` or `appsettings.local.json` where the secret information for the tests will be inserted.
For local development, you should create your own appsettings file and fill in these secrets. The file will be ignored while pushing your changes so no secrets are made public.

## Documentation
All the available feature documentation is located under the `docs` folder. If your feature has impact on public functionality, you'll have to change the feature information too.
This will be done in the `./docs/preview` folder of the Arcus library. There you'll find a functional split of the functionality in markdown (`.md`) files.

It should be fairly easy to pinpoint which file you should change for an enhancement or fix. 
For new features, please make sure that you keep the same structure of documentation features:

````
---
title: "Your feature description"
layout: default
---

# Your feature description
Short summary of what this Arcus feature provides.

## Your more detailed functionality
More in-depth description of what the feature does.

```csharp
YourModel test = YourMethod(); 
```
````

> Note that new feature also should be linked in the index page, which is usually called `./docs/preview/index.md`.

___
## THANK YOU you for you future contribution! ♥