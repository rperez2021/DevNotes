---
id: mh6z4ealz4jroa11xmrrjv8
title: Unit Tests
desc: 'Notes on Unit Testing'
updated: 1649727239970
created: 1649702499850
---
## What are Unit tests?

Unit tests exist to test individual units of software functionality. A unit is a module, component, or function. They’re bits of the program that can work independently of the rest of the program. The presence of unit testing implies that the software is designed in a modular fashion. You may hear once in a while that there are ways to make software “more testable.”

If you find that it’s hard to write unit tests for your program without mocking lots of other things, that’s a sign that your program is not modular enough. Revealing tight coupling (the opposite of modularity) is one of the many important roles that unit tests play in software creation.

Every module should have unit tests, and every application should be made up of modules. In other words, if you’re not writing unit tests, you should be.

When you write a bug report, you should always provide a description, explain what you expected to see, and explain what you actually saw.

Test cases should be written in much the same way:

- Describe the feature that you’re testing in plain English.
- Provide the expected outcome of the test. This part is why many unit tests are called expectations.
- Compare that to the actual value.
- When a unit tests fails, the error message is your bug report.

Simple tests assertions provide:

- Better readability.
- Less code.
- Less maintenance.

## Unit Test Goals

- Thorough
- Stable
- Fast
- Few
