# Testing Rationale

## Why automatic tests?
1. You can make incremental updates to your code more quickly.
2. You can refactor your code with greater confidence.
3. It leads to better designed code.
4. They prevent recurring bugs (bug regressions).
5. They let you blame other people (contract-based development).
6. Other people can work on your code more easily (an automatic form of documentation).
7. It's much easier to become a contributor if we have automated unit tests.
8. Automatic tests simplify maintainer-ship.
9. Automatic tests amplify the value of continuous integration.

## What makes good tests?
1. Tests should be *independent* and *repeatable*.
2. Tests should be well *organized* and reflect the structure of the tested code.
3. Tests should be *portable* and *reusable*.
4. When tests fail, they should provide as much *information* about the problem as possible
5. The testing framework should liberate test writers from housekeeping chores and let them focus on testing *content*.
6. Test should be *fast*.
