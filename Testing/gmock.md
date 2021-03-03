# gMock

## Fake object vs Mock object
* **Fake** objects have working implementations, but usually take some shortcut (perhaps to make the operations less expensive),
  which makes them not suitable for production. An in-memory file system would be an example of a fake.
* **Mocks** are objects pre-programmed with expectations, which form a specification of the calls they are expected to receive.

## Reference
[googletest/gmock_for_dummies.md at master · google/googletest](https://github.com/google/googletest/blob/master/docs/gmock_for_dummies.md)
