# Testing Rationale

## Why automatic tests?
1. Prove that code works like I think it should
2. You can make incremental updates to your code more quickly.
3. You can refactor your code with greater confidence.
4. It leads to better designed code.
5. They prevent recurring bugs (bug regressions) by providing a safe net for future changes.
6. They let you blame other people (contract-based development).
7. Other people can work on your code more easily (an automatic form of documentation).
8. It's much easier to become a contributor if we have automated unit tests.
9. Automatic tests simplify maintainer-ship.
10. Automatic tests amplify the value of continuous integration.

## What makes good tests?
1. Tests should be *independent* and *repeatable*.
2. Tests should be well *organized* and reflect the structure of the tested code.
3. Tests should be *portable* and *reusable*.
4. When tests fail, they should provide as much *information* about the problem as possible
5. The testing framework should liberate test writers from housekeeping chores and let them focus on testing *content*.
6. Test should be *fast*.

## Four Phases of Testing
1. Setup (Arrange)
2. Exercise (Act)
3. Verify (Assert)
4. Cleanup
