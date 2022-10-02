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



## Reasons for Testing

> **Confidence**:
When we are practicing CI/CD, any code that successfully passes through our CI pipeline indicates our teams confidence that this code is ready for the next environment. We always treat the next environment *as if* it were **Production**. The tests themselves become an expression of our teams understanding of business requirements, and therefore become the focus of conversation when discussing changing requirements, or highlighting places we have misunderstood those requirements.

> **Team Support**:
> Our tests become the *reliable* documentation for other developers on our team. Our tests become the expression of our understanding of the business requirements. They provide *guardrails* to guide other developers in adding or changing functionality, allowing regressions in functionality to be detected early. Our type system and our static testing tools provide a sort of "culture" for our particular code base, allowing new developers to easily be introduced to our code base.

## Our Process

The following testing techniques are presented roughly in the order we, as developers, relate to the testing process. 

### Static Testing

We start by *leaning into* the inner-loop feedback we get from our development tools in a "live" way while we write our application. In Angular, we write our code in a combination TypeScript, HTML Templates, and CSS.

#### ESLint

```shell=
ng add @angular-eslint/schematics
```

#### The TypeScript Compiler

The TypeScript compiler can seem like an odd beast, especially for developers coming from strictly typed compiled languages like C# or Java. TypeScript's philsophy is to allow *eventual typing*. Since the output of the TypeScript compiler is JavaScript, and JavaScript does not have a way to annotate data types, and because JavaScript is often the *input* to the compiler, type annotations in "raw" TypeScript are optional. The developer can add type annotations in a sort of *ad-hoc* manner. The initial use-case for TypeScript was to add safety to *existing* JavaScript code and libraries. TypeScript was designed to initially be a "value add". You could rename your JavaScript files (`.js`) to a TypeScript file (`.ts`), and run it through the compiler. Almost any valid JavaScript file is a valid TypeScript file. Developers could then *annotate* their functions, variables, etc. with type information as a way to "harden" their code.

As professional Angular developers the code we write *originates* as TypeScript code. We do *not* often *start* with writing JavaScript. It is imperative that you have a thorough understanding of the TypeScript language.

Seen from this perspective, TypeScript becomes a tool for writing tests. We create data types that describe their valid use.

> :alien: **`TSConfig.json`**
> In Angular projects TypeScript is configured through the `tsconfig.json` file to be more "strict" than the raw TypeScript compiler


**The best way to ensure confidence is to make it impossible for code to do something illegal (e.g. create invalid states) in your application.**


#### ESLint

ESLint is a tool that lets a team create *subjective* rules for their coding style. It is a great way to keep some consistency, and also help developers avoid common pitfalls in coding.

> **Example 1** Strict vs. Implicit Equality

> **Example 2** The `var` keyword is broken. Don't use it.

#### Prettier

Prettier is a *code formatter*. If code is formatted and presented in a consistent way, developers have an easier time reasoning about the code.



#### Angular Language Service

The Angular Language Service and associated VSCode extension goes a long way to making one of the more brittle parts of our application more resilient. 


### Application Integration Testing

These are arguably the most important tests for Angular application developers. 

> **NOTE**: Applications aren't the only thing Angular developers create. What I mean by "application" here is that you are *applying* Angular, libraries, and back-end APIs to solve real business requirements. 

In Application Integration Testing we start by testing the *external* quality of the application. We write tests (scenarios) that demonstrate that the application will allow users to accomplish the things we want them to accomplish.

**Applications** have a benefit in terms of testing other other kinds of code (libraries, etc.) in that the behavior of the application can be **verified** through the user interface.

We can use these kind of test scenarios to ensure that we are **building the right thing**, and then worry about **building it right**.

In this course we will use the Cypress testing tool to do our Application Integration Testing.

It is through the user interface we create in our Angular Application that your users will interact with the application. Good UI and UX design means that we design a UI to *constrain* the user to interactions that map to our business requirements.

For example, if, when filling out a form, a user must select a state code, we *could* just provide a text box where they type in their state code. This could allow the users to enter an invalid code however, which would make our code fail, or we would have to do some `post-hoc` validation, interrupting the application flow. 

> **Definition: Post-Hoc**: What I mean here is "after the event". In this example having a user fill out a form, submit it, and *then* receive an error message is a UI/UX *anti-pattern*. It is almost always preferable to give the user information *as the event happens*. Or, better, not allow the user to make an invalid selection.

Continuing with the example of the state code, giving the user a fixed set of values they can select from is preferable. 

This is the same thinking we applied to writing types in TypeScript. **Do what you can to make invalid states impossible**.

Much of our testing work is just that - ensuring invalid states are not possible. In Angular (and other UI frameworks) the heavy lifting on this is done through the UI.



### Unit Testing

### Component Testing



