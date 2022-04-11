---
id: v9lxey87473adidmtydpf2u
title: TDD
desc: 'Notes on Test Driven Development'
updated: 1649381575417
created: 1649381265266
---
## General Info

**Test-driven development (TDD)**, is a new age evolutionary approach to development which emphasizes test-first development. Here you write a test before you write just enough production code to fulfill that test and then go on to refactor the code. The primary goal of TDD is specification and not validation (Martin, Newkirk, and Kess 2003).  In other words, TDD is one way to think through your requirements or design before your write your functional code (implying that TDD is both an important agile requirements and agile design technique). Another view is that TDD is a programming technique. As Ron Jeffries likes to say, the goal of TDD is to write clean code that works.

The first step is to quickly add a test, basically just enough test for your code to fail. Next you run your tests, often the complete test suite although for sake of speed you may decide to run only a subset, to ensure that the new test does in fact fail. You then update your functional code to make it pass the new tests. The fourth step is to run your tests again. If they fail you need to update your functional code and retest until the tests pass.

![TDD Steps](/assets/tddSteps.jpg)

### Why should developers care about automated unit tests?

- Keeps you out of the (time hungry) debugger!
- Reduces bugs in new features and in existing features
- Reduces the cost of change
- Improves design
- Encourages refactoring
- Builds a safety net to defend against other programmers
- Is fun
- Forces you to slow down and think
- Speeds up development by eliminating waste
- Reduces fear

### How does TDD take development to the next level?

- Improves productivity by
  - minimizing time spent debugging
  - reduces the need for manual (monkey) checking by developers and tester
  - helping developers to maintain focus
  - reduce **wastage**: hand overs
- Improves communication
- Creating living, up-to-date specification
- Communicate design decisions
- Learning: listen to your code
- Baby steps: slow down and think
- Improves confidence
- Testable code by design + safety net
- Loosely-coupled design
- Refactoring

In summary, the importance of TDD cannot be overemphasized. TDD means less bugs, higher quality software, and a razor focus, but it can slow development down and the test suites can be tedious to manage and maintain. All in all, it is a recommended approach as the Pros far outweighs the Cons.
