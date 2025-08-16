[[operating systems]]

- Take physical resources and transform them into virtual representation
- - makes each program think it has each resource to itself.

Virtualizing the CPU 
- Turn single cpu into illusion of ‘infinite’ cpu’s
- Allow many programs to appear to all run at the same time
CPU virtualization

- One often wants to run more than one program at the same time
- A single cpu is a finite resource
- - how does the os allow it to run many programs at once
- - it provides an illusion that an infinite number of cpus exist

- most fundamental abstraction the os provides is the process

Cpu policy is what decides what program to run first in a multi program queue

Virtualizing [[memory]]

- Physical memory is an array of bytes
- A program keeps all its data structures in memory
- Allows every program to think it has all the memory to itself.

