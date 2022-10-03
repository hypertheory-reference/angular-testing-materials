---
title: Course Overview
tags: Angular, Testing
---

# Angular Developer Testing

"Developer Testing" is what we do in the "inner loop" - tests we run on our local developer machine as part of creating our Angular application.

This includes:

- Static Testing
  - TypeScript type System, ESLint, Prettier, Etc.
- Unit Testing
  - Testing isolated units of code.
- Component Testing
  - Testing compiled Angular Componenents in Isolation
- Application Integration Testing
  - Testing the application through the UI

## Why Test?

For software developers, we write tests to fill gaps in the ability of our language and tools to ensure that our software meets the requirements and to _demonstrate our understanding of the requirements_.

Through tests, we gain:

> **Confidence**:
> When we are practicing CI/CD, any code that successfully passes through our CI pipeline indicates our teams confidence that this code is ready for the next environment. We always treat the next environment _as if_ it were **Production**. The tests themselves become an expression of our teams understanding of business requirements, and therefore become the focus of conversation when discussing changing requirements, or highlighting places we have misunderstood those requirements.

> **Team Support**:
> Our tests become the _reliable_ documentation for other developers on our team. Our tests become the expression of our understanding of the business requirements. They provide _guardrails_ to guide other developers in adding or changing functionality, allowing regressions in functionality to be detected early. Our type system and our static testing tools provide a sort of "culture" for our particular code base, allowing new developers to easily be introduced to our code base.

> **Designing a Solution**:
> Sometimes we write tests to guide our development of code with algorithmic complexity. Using a _test-first_ or _tdd_ approach, we write tests to help us think through the solution to a problem.

## Our Process

The following testing techniques are presented roughly in the order we, as developers, relate to the testing process.

### Static Testing

We start by _leaning into_ the inner-loop feedback we get from our development tools in a "live" way while we write our application. In Angular, we write our code in a combination TypeScript, HTML Templates, and CSS.

#### The TypeScript Compiler

The TypeScript compiler can seem like an odd beast, especially for developers coming from strictly typed compiled languages like C# or Java. TypeScript's philsophy is to allow _eventual typing_. Since the output of the TypeScript compiler is JavaScript, and JavaScript does not have a way to annotate data types, and because JavaScript is often the _input_ to the compiler, type annotations in "raw" TypeScript are optional. The developer can add type annotations in a sort of _ad-hoc_ manner. The initial use-case for TypeScript was to add safety to _existing_ JavaScript code and libraries. TypeScript was designed to initially be a "value add". You could rename your JavaScript files (`.js`) to a TypeScript file (`.ts`), and run it through the compiler. Almost any valid JavaScript file is a valid TypeScript file. Developers could then _annotate_ their functions, variables, etc. with type information as a way to "harden" their code.

As professional Angular developers the code we write _originates_ as TypeScript code. We do _not_ often _start_ with writing JavaScript. It is imperative that you have a thorough understanding of the TypeScript language.

Seen from this perspective, TypeScript becomes a tool for writing tests. We create data types that describe their valid use.

> :alien: **`TSConfig.json`**
> In Angular projects TypeScript is configured through the `tsconfig.json` file to be more "strict" than the raw TypeScript compiler

**The best way to ensure confidence is to make it impossible for code to do something illegal (e.g. create invalid states) in your application.**

#### ESLint

ESLint is a tool that lets a team create _subjective_ rules for their coding style. It is a great way to keep some consistency, and also help developers avoid common pitfalls in coding.

> **Example 1** Strict vs. Implicit Equality

> **Example 2** The `var` keyword is broken. Don't use it.

#### Prettier

Prettier is a _code formatter_. If code is formatted and presented in a consistent way, developers have an easier time reasoning about the code.

#### Angular Language Service

The Angular Language Service and associated VSCode extension goes a long way to making one of the more brittle parts of our application more resilient.

### Application Integration Testing

These are arguably the most important tests for Angular application developers.

> **NOTE**: Applications aren't the only thing Angular developers create. What I mean by "application" here is that you are _applying_ Angular, libraries, and back-end APIs to solve real business requirements.

In Application Integration Testing we start by testing the _external_ quality of the application. We write tests (scenarios) that demonstrate that the application will allow users to accomplish the things we want them to accomplish.

**Applications** have a benefit in terms of testing other other kinds of code (libraries, etc.) in that the behavior of the application can be **verified** through the user interface.

We can use these kind of test scenarios to ensure that we are **building the right thing**, and then worry about **building it right**.

In this course we will use the Cypress testing tool to do our Application Integration Testing.

It is through the user interface we create in our Angular Application that your users will interact with the application. Good UI and UX design means that we design a UI to _constrain_ the user to interactions that map to our business requirements.

For example, if, when filling out a form, a user must select a state code, we _could_ just provide a text box where they type in their state code. This could allow the users to enter an invalid code however, which would make our code fail, or we would have to do some `post-hoc` validation, interrupting the application flow.

> **Definition: Post-Hoc**: What I mean here is "after the event". In this example having a user fill out a form, submit it, and _then_ receive an error message is a UI/UX _anti-pattern_. It is almost always preferable to give the user information _as the event happens_. Or, better, not allow the user to make an invalid selection.

Continuing with the example of the state code, giving the user a fixed set of values they can select from is preferable.

This is the same thinking we applied to writing types in TypeScript. **Do what you can to make invalid states impossible**.

Much of our testing work is just that - ensuring invalid states are not possible. In Angular (and other UI frameworks) the heavy lifting on this is done through the UI.

### Unit Testing

Unit tests test only units (methods, or functions, usually) in _isolation_ from their dependencies. This means we are testing only our code not other code (e.g. library code, framework code, etc). We may test how our code _interacts_ with other code, but that code is not evaluated as part of our tests.

As application developers, when we take a dependency on another library or framework, part of the evaluation process that is involved in taking that dependency is on the reliability of that library or framework. We may, for example, check to see if the code we wish to include contains it's own set up of tests. Once we are confident of the reliability of that code, we take a dependency on it (in Angular, through NPM), and we _trust_ it. That means we don't:

- Run the dependencies tests as part of our workflow.
- Write tests that involve that code directly, or exercise its behavior.

_If_ a defect is found in that code, and it is open source, we should clone the repository for that code, find the defect, and provide a fix, with associated tests, as a pull request. At the very least we should file an issue with the team responsible for the code.

> **Important**: If your tests have _intimate_ knowledge of the libraries or frameworks you are using, you do not have sufficient isolation in your tests.

### Component Testing

Sometimes in your work as an Angular application developer you will create libraries. This usually means you are extracting some code for a specific, bounded, controlled _application_ and generalizing it for others to use.

For example, you might create a component that displays information about the logged in user as part of your work in creating the application. Other developers on your team may try to reuse that code. It could be a crude "copy and paste" job, or they simply start referencing your component in their components.

_Because_ you created the component for a specific application, there may be implicit edge-cases that can cause the component to behave poorly if the context in which it is used is different than your context.

An example would be that your component takes an input of type `UserInformation`. In your use, there is no case where that input will be `null` or `undefined`. There was no reason to test for that, as you could verify the behavior through an application integration test.

Another example might be part of your component displays some details about when the user onboarded. Think "member since: July 2022". Your component _assumes_ the property on the `UserInformation` type is a legitimate ISO-8601 date representation. However other parts of your application might format dates in different ways.

In these cases, it's best to _extract_ the component to a library module, and write tests that demonstrate it's use in it's "extracted" (i.e. extracted from the context it was created for) modes.

You start with testing and proving your context.

And then you (or other developers using the component) can _add_ tests that demonstrate the proper behavior in _other_ contexts.
