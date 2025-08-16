[[operating systems]]

- Events are occurring simultaneously and may interact with each other or same resources
- Os must be able to handle the concurrent events. Not only limited to the os, modern, multithreaded applications exhibit the same problems.
- Easiest case - hide concurrency from independent process
- Harder case - manage concurrency with interacting processes - provide abstractions (locks, semaphores, shared memory etc.) Ensure processes do not deadlock