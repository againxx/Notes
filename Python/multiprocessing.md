# Multiprocessing

* Multiprocessing can effectively side-stepping the Global Interpreter Lock (GIL) by using subprocesses instead of threads
* GIL is an implementation limitation of CPython instead of the limitation of Python language

## Three ways to start a process
### spawn
* The parent process starts a **fresh** python interpreter process.
* The child process will only inherit those resources necessary to run the process object's `run()` method.
* Rather **slow** compared to using `fork` or `forkserver`
* default on Windows and macOS

### fork
* The parent process use `os.fork()` to fork the Python interpreter.
* The child process is identical to the parent process. All resources of the parent are inherited by the child process.
* Safely forking a **multithreaded** process is problematic.
* Available on Unix only. The default on Unix.

### forkserver
* When the program starts with the *forkserver* start method, a server process is started
* The parent process connects to the server and requests that it fork a new process.
* The fork server process is single threaded so it's safe for it to use `os.fork()`
* No unnecessary resources are inherited (how about parent process's resources, how will it be transferred to the child?)
* Only on Unix which support passing file descriptors over pipes

```python
import multiprocessing as mp

def foo(q):
    q.put('hello')

if __name__ == '__main__':
    mp.set_start_method('spawn')
    q = mp.Queue()
    p = mp.Process(target=foo, args=(q,))
    p.start()
    print(q.get())
    p.join()
```

### context
* Since `set_start_method()` should not be used more than onece in general program, we can use `get_context()` to obtain a context object
* Context objects have the same API as the multiprocessing module, and allow using multiple start methods in the same program
