
2025-08-11 20:09

Status:

Tags: 

# Operating systems

recreating notes from my operating system class here


-The operating system is the middle ground between hardware and software.  
-manages the use of hardware and shares it between the software

Roles of what the os provides

1. Abstraction

- Splits simultaneous tasks onto the cpu to run them
- Such as if 4 tasks need to run, the os decides what and when the program will be running on the cpu and when it is being stopped so another can run on the cpu.

2. Resource management

- Figures out how to allow the programs to use the full memory when running. Such as maybe writing something else on memory onto the disk to free space.

[[Virtualization]]

[[Concurrency]]

[[Persistence]]



[[C]]
Compiling $ gcc -Wall -Werror -o (name)  
Running ./(name) (inputs)



Machine state - what process can read or update while its running  
[[Memory]]

[[CPU]] context: registers

- Program counter (pc) sometimes called instruction pointer (ip)
- Stack pointer and frame pointer

File descriptors

Process API

- Create (create a process somehow)

`fork()
`xec()

- Destroy

Kill  
`SIGINT,SIGHUP,SIGSTP`

- Wait

`wait()`

- Miscellaneous control
- Status

Processing states

Ready -> (scheduled) -> Running or (descheduled) -> Ready

Running -> (initiate)-> Blocked -> done

[[Operating Systems Data Structures]]


Cpu virtualization  
How to provide good performance

- Direct execution
- - allow user process to run directly on hardware
- - os creates process and transfers control to starting point

Os:

1. Create entry process list
2. Allocate memory for program
3. Load program into memory
4. Set up stack with argc / argv
5. Clear registers
6. Execute call main()

Program:

7. Run main()
8. Execute return from main()

Os:

9. Free memory of process
10. Remove from process list

Problem 1: restricted operations

[[System Calls]]

Problem 2: switching between processes

- How can the os regain control of the cpu so it can switch between processes
- 1. A cooperative approach: wait for the process to yield control or system calls
- 2. A non cooperative approach …

Cooperative approach: os waits for system calls

- Processes periodically give up the cpu by making systems calls such as yield
- 1. The os divides to run some other task
- 2. application also transfer control to the os when they do something illegal
- - such as divide by 0
- - try to access memory that it shouldnt be able to access
- ex) early versions of the macintosh os, the old xerox alto system

Non cooperative approach: os takes control

- A timer interrupt
- 1. During the boot sequence, the os starts a timer
- 2. The timer raise an interrupt ever so many milliseconds
- 3. When the interrupt is raised:
- - the currently running process is halted
- - save enough of the state of ther program
- - a preconfigured interrupt handler in the os runs

Context switch

- Scheduler makes a decision:
- 1. Whether to continue running the current process, or switch to a different one
- 2. If the decision is made to switch, the os executes context switch

Context switch: a low level piece of assembly code

- Save a few register values for the current process onto its kernel stack
- 1. General purpose registers
- 2. Pc
- 3. Kernel stack pointer

Restore a few for the soon to be executing process from its kernel stack  
Switch to the kernel stack for the soon to be executing process

Worried about concurrency

- What happens if, during interrupt or trap handling, another interrupt occurs?
- - topic for the second piece of os: concurrency

- the OS handles these situations  
- disables interrupts during interrupt processing  
- use a number of sophisticated …

[[Schedulers]]


Proper data structures

- One major focus of cfs is efficiency
- Simple data structures like lists dont scale
- Cfs addresses by using red-black trees
- Only stores processes that are running

Dealing with i/o and sleep

- One problem with picking lowest vruntime is processes that have gone to blocked
- Imagine two processes a and b

1. A runs continuously
2. B goes to sleep for a long period
3. When b wakes up it will be 10 seconds behind a and then starve a

- Cfs fixes by changing vruntime …..

Memory virtualization —------------------------------------------------  
What is memory virtualization?

- Os provides an illusion that each process has all the memory in the system.
- Os provides a virtual address to program that maps to real memory addresses, running program has no idea

Benefits

- Ease of use -> each program just sees a big contiguous memory space

Early systems  
Early machines did not provide much abstraction

- Os was in memory starting at 0 → 64kb
- Load one process into memory at 64kb and let process use rest of memory
- Poor utilization and efficiency
- To switch between processes must save memory to disk (slow) and load next process into memory from disk (slow)

Multiprogramming and time sharing

- People began to expect more from their machines, era of multiprogramming was born
    
- Load multiple processes into memory
    
- - run one for a short while
    
- - switch to another process in memory
    
- - increase utilization and efficiency
    

Then people expected even more and time sharing was born

- Interactivity became important → many people using machine at once

Address space

- Os creates an abstraction of physical memory
- Code
- - where instructions live
- Heap
- - dynamically allocate memory
- – malloc in c language
- – new in object-oriented language
- Stack
- - store return addresses or values
- - contain local variables arguments to routines

Memory virtualization goals  
Transparency

- Processes are not aware that memory is shared
- Works regardless of number and/or location of processes

Protection

- Cannot corrupt os or other processes
- Privacy: cannot read data of other pcoesses

Efficiency

- Do not wase memory resources (minimize fragmentation)

Sharing

- Cooperating processes can share portions of address space
```

Memory api:malloc()  
#include <stdlib.h>  
void* malloc(size_t size)

Allocate a memory region on the heap

- Argument  
    Size_t size: size of the memory block(in bytes)  
    Size_t is an unsigned integer type

Return

- Success : a void type pointer to the memory block allocated by malloc
- Fail: a null pointer

Char *pointer = (char *) malloc(10*sizeof(char*))

Whatever the size of a character pointer is times 10

realloc() allows a resize of memory
```

Common problems / errors

Forgetting to initialize memory with malloc → segmentation fault  
Not allocating enough memory → buffer overflow  
Forgetting to initialize memory → uninitialized read  
Forgetting to call free() to deallocate memory → memory leak  
Freeing memory before you are done with it → dangling pointer  
Freeing memory repeatedly → double free

Memory virtualization takes a similar strategy known as limited direct execution (lde) for efficiency and control

- Get out of the way as much as possible

In memory virtualizing efficiency and control are attained by hardware support

- Eg registers tlb(translation look-aside buffer) page table

Address translation: hardware transforms a virtual address to a physical address

- The desired information is actually stored in a physical address

The os must get involved at key points to set up the hardware

Address translation

Void func() {  
Int x;  
…  
X = x + 3 // this is the line of code we are interested in  
}

- Load a value from memory (int x)
- Increment it by 3 (x = x + 3)
- Store the value back into memory

128: movl 0x0(%ebx), %eax ; load value at memory address 0+ebs into eax  
132: addl $0x03, %eax ; add 3 to eax register  
135: movl %eax, 0x0(%ebx) ; store eax back to memory

When instructions are run, from view of process following memory access

- Fetch instruction at address 128
- Execute instruction (load from address 15kb)
- Fetch instruction at address 132
- Execute this instruction (no memory reference)
- Fetch the instuction at address 135
- Execute the instruction (store to address 15kb)

From process perspective, memory starts at address 0

- Os wants to place somewhere else in physical memory, not at address 0

When a program starts running, the os decided where in physical memory a process should be loaded

- Set the base register a value  
    Physical address = virtual address + base
    
- Every virtual addres must not be greater than bound and negative
    
    ```
      	0 \<= virtual addressvirtual address \< bounds
    ```
    

Os issues for memory virtualization

The os must take action to implement base and bounds approach  
Three critical juncutres:

- When a process starts running:
- Finding space for address space in physical memory

When a process is terminated:

- Reclaiming the memory for use

When context switch occurs:

- Saving and storing the base and bounds pair

Os issues when a process starts running

The os must find a room for a new address space

- Free list: a list of the range of the physical memory which are not in use

Os issues when a process is terminated

- The os must put the memory back on the free list

Os issues when context switch occurs

The os must save and restore the base and bounds pair

- In process structure or process control block (pcb)

Inefficiency of the base and bound approach

Big chunk of ‘free’ space  
‘Free’ space takes up physical memory  
Hard to run when an address space does not fit into physical memory

Segment is just a contiguous portion of the address space of a particular length.

- Logically-different segment: code, stack, heap

Each segment can be placed in different part of physical memory

- Base and bounds exist per each segment

Address translation on segmentation

The offset of virtual address 100 is 100

- The code segment starts at virtual address 0 in address space

Segmentation fault or violation

If an illegal address such as 7kb which is beyond the end of heap is referenced, the os occurs segmentation fault.

- The hardware detects that address is out of bounds

Support for sharing

Segment can be shared between address sace

- Code sharing is still use in systems today
- By extra hardware support

Extra hardware support is needed for form of protection bits

- A few more bits per segment to indicate permissions of read, write and execute

Example is on slide ch 8

Fine grained and coarse grained

Coarse grained means segmentation in a small number.

- Eg. code, heap, stack

Fine-grained segmentation allows more flexibility for address space in some early systems.

- To support many segments, Hardware support with a segment table is required

Os support fragmentation

External fragmentation: little holes of free space in physical memory that make difficulty to allocate new segments.

- There is 24kb free, but not in one contiguous segment
- The os cannot satisfy the 20kb request

Compation: rearranging the existing segments in physical memory

- Compaction is costly
- Stop running process
- Copy data to somewhere
- Change segment register value

Paging introduction

Paging splits up address space into fixed sized unit called a page…

Advantages of paging

Flexibility: supporting the abstraction of address space effectively

- Dont need assumption how heap and stack grow and are used

Simplicity: ease of free-space management

- The pagein address space and the page frame are the same size
- …

Two components in the virtual address

- vpn : virtual page number
- Offset:...

Where are page tables stored?

Page tables can get large

- 32 bit address space with 4kb pages, 20 bits for vpn
- 4mb = 2^20 entries * 4 bytes per page table entry

Imagine there are 100 processes running → lots of memory being eaten up

What is actually in the page table  
The page table is just a data structure that is used to map the virtual address to physical address

- Simplest form: a linear page table, an array

The os indexes the array by the vpn, and looks up the page table entry (pte)

Flags of page table entry

Valid bit: indicating whether the particular translation is valid.

- For ex: when program starts running heap on one end, stack at other, all space in between marked as invalid
- Protection bit: indicating whether the page could be read from, written to, or executed from
- Present bit: indicating whether this page is in physical memory or on disk(swapped out)
- Dirty bit: indicating whether the page has been modified since it was brought into memory
- Reference bit(accessed bit): indicating that a page has been accessed

Paging: faster translations  
When we want to make things fast, the os usually needs some help → Hardware

To speed up address translation → translation-lookalike buffer (tlb)

- Part of the chips memory management unit (mmu)
- A hardware cache of popular virtual to physical address translation
- Better name might be address-translation cache

Use caching when possible  
Idea behind hardware caches it to use locality in instruction and data references  
Temporal locality…

Who handles the tlb miss  
Hardware handle the tlb miss entirely on CISC (complex instruction set)

- People who built hardware didnt trust os people
- The hardware had to know exactly where the page tables are located in memory (page table based register)
- The hardware would ‘walk’ the page table, find the correct page-table entry and extract the desired translation, update and retry instruction.
- Example of older hardware-managed tlb is intel x86 which uses multi level page table

RISC have what is known as sofware-managed tlb

- On a tlb miss, the hardware raises exception (trap handler)
- Trap handler is code within the os that is written with the express purpose of handling tlb miss

TLB contents: Whats in there  
Tlb is managed by full associative method

- Basically means any give translations can be anywhere in the tlb
- A typical tlb might have 32, 64, 128 entries
- Hardware search the entire tlb in parallel to find the desired translation

Issue: replacement policy

Cache replacement - specifically when we put new entry in tlb we have to replace an old one.

- We will study when we tackle the problem of swapping pages to disk, couple typical policies include;

LRU(Least Recently Used)

- Evict an entry that has not recently been used
- Take advantage of locality in the memory reference stream

Random

- Evict an entry at random
- Simple and avoids “Corner cases”

Paging review  
Pages are often too big and use too much memory  
A simple solution is to make bigger pages therefor reducing the number of pages/entries  
Now a page will use 1mb per page vs 4mb before  
Introduces internal fragmentation

Hybrid approach: Paging and segments  
To reduce the memory overhead of page tables

- Using base not to point to the segment itself but rather to hold the physical address of the page table of that segment
- The bounds register is used to indicate the end of the page table (how many valid pages it has)

Each process has three page tables associated with it.

- When process is running, the base register for each of these segments contains the physical address of a linear page table for that segment

Tlb miss for hybrid approach  
The Hardware get to physical address from page table

- The hardware uses the segments bits (sn) to determine which base and bounds pair to use.
- The hardware then takes the physical address therein and combines it with the vpn and follows to form the address of the page table entry (PTE)

Problems  
Hybrid approach is not without problems

- Still requires us to use segmentation which isnt quite as flexible as we’d like as it assumes a certain usage pattern of address space.
- If we have a large but sparsely used heap, we can still end up with a lot of page table waste

Causes external fragmentation to arise again

- While most memory is managed in page sized unit, page table now can be of arbitrary size (in terms of pages), thus finding free space for them becomes more complicated

Advantages

- Only allocates page table space in proportion to the amount of address space you are using
- The os can grab the next free page when it needs to allocate or grow a page table → level of indirectoin
- Contrast to linear which requires contiguous block for entire page table

Disadvantages

- Multilevel table is a small example of a time-space tradeoff → on tlb miss two memory reads will be required (cache misses are less efficient)
- Complexity → whether hardware or os handling tlb miss process is more complex than a simple linear table

Detailed multilevel example  
-Our page table in this example is 256 entries spread across 16 pages  
– page directory needs one entry page page of page table, thus 16 entires  
We can represent this in the first 4 bits of vpn in virtual address  
Once we extract page directory index from vpn can be used to find address of the page directory

- PDEAddr = pageDirBase + (PDIndex * sizeof(PDE))
- Page directory entry

If the PDE is valid, we have more work to do:

- fetch the page table entry (PTE) from the page of the page table pointed to by this page directory entry
- This page table index can then be used to index into the page table itself
- PTEAddr = (PDE.PFN << SHIFT) + (PTIndex + sizeof(PTE))
- Page from number (PFN from page directory entry must be left shifted before combining with the page table index to form the address of the PTE

00011111010101

Pde → 0001 = 1 - 1 = 0 using index 0 = pfn 100 in example  
Pfn → 100

Next four bits for pte  
→ 1111 = 16 - 1 = 15

This example tried to reference invalid memory, segmentation fault.

More than two level: page directory  
If our page has 2^14 entries, it spans no one page but 128

- Remember out goal is to make every piece of the multi-level page table fit into a page

To remedy this problem, we build a further level of the tree, by splitting the page directory itself into multiple pages of the page directory.  
Use upper level bits of virtual address (PD index 0) to fetch the page

Inverted page tables

- Even more extreme form of space saving is called inverted page tables
- Keeping a single page table that has an entry for each physical page of the system instead of having many page tables (one per process)
- The entry tells us which process is using this page, and which virtual page of that process maps to this physical page

Beyond physical memory: mechanisms

Require an additional level in the memory hierarchy

- Os needs a place to stash away portions of address space that currently arent in great demand
- In modern systems this role is usually served by a hard disk drive

Fastest to slowest hierarchy  
Registers → cache → main memory → mass storage (disk)

Swap space

Reserve some space on the disk for moving pages back and forth → in modern os this is called swap space

Assume that the os can read and write from swap in page-sized units

- Os must remember disk address of a given page

Present bit

Lets assume a hardware managed tlb, what happens on a member reference

If we wish to allow pages to be swapped to disk, must add some machinery

Present bit - bit in the TLE to determine if page is in physical memory

1 = page is present in physical memory  
0 = page is not in memory but rather on disk

What if memory is full

Page in - os brings memory from disk to physical memory  
Page out - os must kick out

When replacements really occur

Os waits until memory is entirely full, and only then replaces a page to make room for some other page

- This is a little bit unrealistic, and there are many reasons for the os to keep a small portion of memory free more proactively

To keep a small amount of memory free, most os have High watermark (HW) and low watermark (LW)

Swap Daemon (aka page Daemon)

- There are fewer than LW pages available, a background thread that is responsible for freeing memory runs
- The thread evicts pages until there are HW pages available
- Then thread goes to sleep

Optimization

Missed some slides 10/4

Common threading models  
Multi threaded programs tend to be structured as:  
producer/consumer

- Multiple producer threads create data (or work) that is handled by one of the multiple consumer threads

Pipeline

- Task is divided into series of subtasks, each of which is handled in series by a different thread

Defer work with background thread

- One thread performs non critical work in the background (when cpu idle)

Address space changes, there is a stack for each thread with free space in between them for the lower stack to grow.

Thread demo 1  
Scheduling was changing and undeterministic  
Thread demo 2  
For loop to a million with a counter = counter +1  
Variables are not atomic, (only to one cpu) so one thread was overwriting the second thread counter variable when running so counter would change sporadically with the program.

Critical section  
A piece of code that access a shared variable and mst not be concurrently executed by more than one thread

- Multiple threads executing critical section can results in rance condition
- Need to execute atomically for critical sections (mutual exclusion)

Could use single instructions in cpu

- Not great for complex use cases
- Instead use a few instructions to build a general set of synchronization primitives
- monitors , locks, semaphores, condition varaibles

Thread api creation

#include <pthread.h>  
Int pthread_Create(...

Thread: used to interact with this thread  
Attr: used to specify any attributes this thread might have

- Stack, size, scheduling priority

Start_routine: the function this thread starts running in  
Arg: the argument to be passed to the function(Start routine)

- A valid pointer allows us to pass in any type of argument

Dangerous code  
Be careful with how values are returned from a thread  
When the variable r returns, it is automatically deallocated

Locks  
Provide mutual exclusion to a critical section of code  
Int pthread_mutex_lick(pthread_mutex_t *mutex);  
Int pthread_mutex_unlock(pthread_mutex_t *mutex);

Usage (w/o lock initialization and error check)

Pthread_mutex_t lock;  
pthread_mutex_lock(&lock);  
x=x+1; //critical section  
pthread_mutex_unlock(&lock);

All locks must be properly initialized

One way using pthread_mutex_initializer  
Pthread_mutex_t lock = PTHREAD_MUTEX_INITALIZER;

The dynamic way: ……..

These two calls are also used in lock acquisition  
Trylock: return failure ig the lock is already held  
Timelock: return after a timeout or after acquiring the lock

Locks basic ideas  
Ensure that any critical section executes as if it were a single atomic instruction

- An example updating a shared variable above

Add code around the critical section to lock it  
Lock_t mutex;  
…  
lock(&mutex…….

Lock variables hold the state of the lock

- Available or unlocked or free
- No thread holds the lock

Acquired or locked or held

- Exactly one thread holds the lock and presumably is in a critical section.

The name that the posix library uses for a lock

- Used to provide mutual exclusion between threads

Pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER;

pthread _mutex_lock(&lock);  
Balance = balance + 1; //critical section  
pthread _mutex_unlock(&lock);

We may be used different locks to protect different variables → increase concurrency (a more fine grained approach)

Building a lock

Efficient locks provided mutual exclusion at low cost  
Building a lock need some help from the hardware and the os  
Lock evaluation criteria

Mutual exclusion

- Does the lock work, preventing mulitple threads from entering a critical section

Fairness

- Does each thread contending for the lock get a fair shot at acquiring it once it is free? (starvation)

Performance

- The time overheads added by using the lock

Increasing performance  
Simple solution: control interrupts  
Disable interrupts for critical sections

- One of the earliest solutions used to provide mutual exclusion
- Invented for single-processor systems

Problem

- Require too much trust in application
- Greedy or malicious program could monopolize the processor
- Does not work on multiprocessors
- Code that masks or unmasks interrupts be executed slowly by modern CPUS

Void lock(){  
disableinterrupts();  
}

Void unlock(){  
Enable interrupts();  
}

Why do we need hardware support  
First attempt: using a flag denoting whether the lock is held or not

- The code below has problems, what are they

Typedef struct __lock_t {int flag;} lock_t;

Void init(lock_t *mutex){  
//0 → lock available, 1 → held  
mutex-> flag = 0;  
}

Void lock(lock_t *mutex){  
While (mutex->flag == 1);  
mutex->flag = 1;  
}

Void unlock(lock_t *mutex){  
Mutex -> flag = 0;  
}

This is not an atomic process  
See slide for example on how interrupts can cause interference between threads

We need an atomic instruction supported by hardware

- Test and set instruction also known as atomic exchange

Test and set (atomic operation)  
An instruction to support the creation of simple locks

Int TestAndSet(int *ptr, int new){  
Int old = *ptr //fetch old value at ptr  
*ptr = new; //store new into ptr  
Return old;  
}

If old ptr is 1 that means some thread is already doing some operation somewhere, this is why we return the old value

Evaluating spinlocks  
Correctness: yes

- Spin lock only allows a single thread to enter the critical section

Fairness; no

- Spinlocks dont provide any fairness guarantees
- Indeed a thread spinning may spin forecter

Performance

- In the single cpu, performance overheads are large
- If the number of thread roughly equals the number of cpus, spin locks work reasonable well

Compare and swap  
Test whether the value at the address(ptr) is equal to expected

- If so, update the memory location pointed by ptr with the new value
- In either case, return the actual value at that memory location

Load linked and store conditional  
The store conditional only succeeds if no intermittent store to the address has taken place

- success : retu…..

Fetch and add  
Atomically increment a value while returning the old value at a particular address

Int FetchandAdd (int *ptr)P  
Int old = *ptr;  
*ptr = old +1  
……. Bruh is going to fast look at slides

Ticket lock  
Ticket lock can be built with fetch and add

- Ensure progress for all threads → fairness

Typedef struct __lock_t{  
Int ticket;  
Int turn;  
} lock_t;  
……………keeps oging look at slide

Hardware based spin locks are simple and they work

In some cases these solutions can be quite inefficient

- Any time a thread gets caught spinning, it wastes an entire time slice doing nothing but checking a value

A simple approach: just yield

When you are going to spin, give up the cpu to another thread

- Os system call moves the caller from the running state to the ready state
- The cost of a context switch can be substantial and the starvation problem still exists

Void init(){  
Flag = 0;  
}

Void lock(){  
While (testandset(&............

Using queues: sleeping instead of spinning  
Queue to keep track of which threads are waiting to enter the lock  
park()

- Puts a calling thread to sleep

unpark(threadID)

- Lets thread know its time to go

Look at code in slides

Wakeup/waiting race  
In case of releasing the lock (Thread a) just before the call to park() (thread b) → thread b would sleep forever potentially

Solaris solves this problem by adding a third system call:setpartk()

- By calling this routine, a thread can indicate it is about to park
- If it happens to be interrupted and another thread calls unpark before park is actually called, the subsequent park returns immediately instead of sleeping

Futex  
Linux provides a futex

- Futex_wait (address, expected)
- Put the calling thread to sleep
- If the value at address is not equal to expected, the call returns immediately

Futex_wake(Address)

- Wake one thread that is waiting on the queue

Two phase lock  
A two phase lock realizes that spinning can be useful if the lock is about to be released  
First Phase

- The lock spins for a while, hoping that it can acquire the lock
- If the lock is not acquired during the first spin phase, a second phase is entered

Second phase

- The caller is put to sleep
- The caller is only woken up when the lock becomes free later

Concurrency objectives

Mutual exclusion

- Solved with lockes

Semaphore  
An object with an integer value

- We can manipulate with two routines; sem_wait() and sem_post()
- Initialization

#include <semaphore.h>

Sem_t s;  
sem_init(&s, 0, 1);

Declare a semaphore s and initialize it to value 1  
The second argument, 0, indicates that the semaphore is shared between threads in the same process

Condition variables vs semaphores

Condition valiables have no state (other than waiting queue)

- Programmer must track additional state

Semaphores have state: track integer value

- State cannot be directly……

Semaphore: interact with semaphore

sem_wait()

Int sem_wait(sem_t *s){  
Decrement the value of semaphore s by one  
Wait if value of semaphore s is negative  
}

If the value of the semaphore was one or higher when called sem_wait(), return right away

It will cause the caller to suspend execution waiting for a subsequent post  
When negative, the value of the semaphore is equal to the number of waiting threads.

Sem_post()

Binary semaphores

What should x be  
The initial value should be 1  
Sem_t m;  
sem_init(&m, 0, X); // initialize the semaphore to X; what should X be?

sem_wait(&m);  
//critical section of code  
sem_post(....)

Event based concurrency  
A different style of concurrent programming

- Ised in gui based applications, some types of internet servers

The problem that event based concurrency addresses is two-fold  
Managing concurrency correctly in multi-threaded applications

- Missing locks, deadlock, and other problems can arrive
    
- The developer has little or no control over what is scheduled
    

Event loop  
Wait for something to occur  
When it does, check what type of event it is  
Do the small amount of work it requires

Check whether there are any incoming I/O that should be attended to  
select()

- Lets the server determine that a new packet has arrived and needs processing
- Let the service know when it is ok to reply
- Timeout
- NULL: cause select() to block indefinitely until some descriptor is ready
- 0: use the call to select() to return immediately

The event based server cannot be interrupted by another thread

- With a single cpu and an event based applications
- It is decidedly single threaded
- Thus concurrency bugs coming in threaded problems to not affect in the basic event based approach

What is ab event requires that you issue a system call that night block

- There are no other threads to run: just the main event loop
- The entire server will do just that: block until the call completes
- Waste of resources

In event based systems blocking is never allowed

Solution asynchronous I/O

- Enable an application to issue an I/O requites and return control immediately to the called, before the …

Interrupt

- Remedy the overhead to check whether an I/O has completed
- Using UNIX signals to inform applications when an asynchronous I/O completes
- Removing the need to repeatedly ask the system

Another problem : state management  
The code of event based approach is generally more complicated to write than traditional thread-based code

- It must package up some program state for the next event handler to use when the I/O completes
- The state the program needs is on the stack of the thread → manual stack management

Ex) event based system  
Int rc = read(fd, buffer, size);  
Rc = write(sd, buffer, size);  
……

Solution: continuation  
Record the needed information to finish processing this event in some data structure  
When the event finishes…..

Persistence

I/O devices  
I/O is critical to computer systems to interact with the systems

Canonical devices  
Canonical device has two important components

- Hardware interface allows the system software to control its operation
- Internals which is implementation specific

Status register

- See the current status of the device

Command register

- Tell the device to perform a specific task

….

Polling  
Operating system waits until the device is ready by repeatedly reading the status of the register

- Positive aspect is simple and working
- However it wastes cpu time just waiting for the device
- Switching to another ready process is better utilizing the cpu

Interrupts

- Put the io request process to sleep and context switch to another
- When the device is finished wake the process waiting for the io by interrupt
- Positive aspect is allow to cpu and the disk are properly utilized
- Cpu wastes a lot of time to copy a large chunk of data from memory to the device

Direct memory access (DMA)

- Copy data in memory by knowing “where the data lives in memory, how much data to copy”
- When completed, DMA raises an interrupt, io begins on disk

Device interaction continued

- How does the os interact with different specific interfaces
- ex) wed like to build a file system…….

Hard disk drive  
Hard disk drives have been the main form of persistent data storage in computer systems

- The drive consists of a large number of sectors 512 block
- Address space - we can view the disk with n sectors as an array of sectors; 0 to n-1

Interface

- The only guarantee is that a single sector write is atomic

Multi sector operations are possible

- Many file systems will read or write 4kb at a time
- Torn write - in an untimely power loss occurrs, only a portion of a larger write may complete

Accessing blocks in a contiguous chunk is the fastest access mode

- A sequential read or write
- Much faster than any more random access pattern

Basic geometry of a hard drive

- Platter (aluminum coated with a thin magnetic layer)
- A circular hard surface
- Data is store persistently by inducing magnetic changes to it
- Each platter has 2 sides, each of which is called a surface

Spindle

- Spindle is connected to a motor that spins the patters around
- Rate of rotations is measured in rpm - typical modern values 7200 to 15000
- 10000rpm single rotation takes about 6ms

Track

- Concentric circles of sectors
- Data is encoded on each surface in a track
- A single surface contains many thousands and thousands of tracks

Disk head (one head per surface of drive)

- The process of reading and writing is accomplished by the disk head
- Attached to a single disk arm, which moves across the surface

Rotational delay: time for the desired sector to rotate  
Read sector 0; rotational delay = R/2  
Read sector 5; delay = r-1 (worst case) see diagram on slides

Seek: move the disk arm to the correct track

- Seek time: time to move the head to the track that contains the desired sector

Phases of seek

- Acceleration: the disk arm gets moving
- Coasting: the arm is moving at full speed
- Deceleration: the arm slows down
- Settling: the head is carefully positioned over the correct track - settling time around 0.5, 2ms avg

Transfer  
Final phase of Io

- Data is either read from or written to the surface

Complete io time

- Seek
- Wait for rotational delay
- Transfer

Track skew

- Make sure that sequential reads can be properly services even when crossing track boundaries

Cache (track buffer)  
Hold data read from or written to the disk

- Allows the drive to quickly respond to requests
- Small amount of memory (8 or 16mb)

Write on cache  
Writeback (immediate reporting)

- Acknowledge a write has completed when it has put the data in its memory
- Faster but dangerous

Write through

- Acknowledge a write has completed after the write has actually been written to disk

time(ms)/1 rotation = 1min/10000

1000ms is 1 second

60000/10000  
6ms rotation time

Transfer rate

Transfer rate = 100mb/sec

Time (ms)/1 request

512 kbytes / 1 request

1mb / 1024kb

1 sec / 100 mb

1000ms / 100

5ms / request

Io time: tio = seek +troation + transfer

Rate of io: size of transfer/ t io

Disk scheduling  
Disk scheduler decides which io request to schedule next  
Sstf (shortest seek time first)

- Order the queue of io request by track
- Prick requests on the nearest track to complete first

Elevator (aka scan or c-scan)

Move across the disk servicing requests in order across the track

- Sweep a single pass across the disk
- If a request comes for a block on a track that has already been serviced on this sweep of the disk, it is queued until the next sweep

F-scan

- Freeze the queue to be serviced when it is doing a sweep
- Avoid starvation of far away requests

C-scan

- Sweep from outer to inner, then inner to outer

How to account for disk rotation costs

- If rotation is faster than seek request 16 → request 8
- If seek is faster than rotation request 8 → request 16 sectors = numbers

See slides

Io merging  
Reduce the number of requests send to the disk and lowers overhead

- Eg read blocks 33 , then 8, then 34:
- The scheduler merges the request for blocks 33 and 34 into a single two blocked request

….  
Raid interface

When a raid receives io request

- The raid calculates which disk to access
- The raid issue one or more physical ios to do so

Raid example: a mirrored raid system

- Keep a du…

Raid internals

A microcontroller

- Run firmware to direct the operation of the raid

Volatile memory

- Buffer data blocks

Non volatile memory

- Buffer writes safely

Specialized logic to perform parity calculation

Fault model

Raids are designed to detect and recover from certain kinds of disk faults

Fail-stop fault model

- A disk can be in one of two states: Working or failed
- Working: all blocks can be read or written
- Failed: the disk is permanently lost

Raid controller can immediately observe when a disk has failed

How to evaluate a raid

Capacity

- How much useful capacity is available

Reliability

- How many disk faults can the given design tolerate

Performance

Raid level 0: striping

Raid level 0 is the simplest form as striping blocks

- Spread the blocks across the disks in a round robin fashion
- No redundancy
- Excellent performance and capacity

See slides

Chunk sizes  
Chunk size mostly affects performance of the array

Small chunk size

- Increase the parallelism
- Increasing positioning time to access blocks

Big chunk size

- Reduce intra-file parallelism
- Reducing positioning time

Raid 0 analysis  
Capacity → raid 0 is perfect

- Striping delivers n disks worth of useful capacity

Performance of striping → raid 0 is excellent

- All disks are utlized often

Reliability → none

- If one disk fails all fail

Evaluating raid performance

Consider two performance metrics

- Single request latency
- Steady state throughput

Workload

- Sequential; access 1mb of data (block(b) ~ block (b+ 1mb)
- Random: access 4kb at random logical address

A disk can…

Sequential vs random

- Sequential: transfer 10mb on average as continuous data
- Random: transfer 10kb on average
- Average seek time 7ms
- Average rotational delay 3ms
- Transfer rate of disk 50mb/s

Results  
S = amount of data/time to access = 10mb/210ms = 47.62mb/s  
R = 10kb/10….

Raid level 1: mirroring

Raid level 1 tolerates disk failures

- Copy more than one of each block in the system
- Copy block places on a separate disk

Raid-10 (raid +1): mirrored pairs and then stripe  
Raid -01 (raid 0+1): contain two large striping arrays, and then mirrors

Capacity: raid 1 is expensive

- The useful capacity of raid 1 is n/2

reliability : raid 1 does well

- It can tolerate the failure of any one disk (up to n/2 failures depending on what disks fail)

Two physical writes to complete

- It surfers the worst case seek and rotational delay of the two requests
- Steady state throughput

Squential write : n/2 * sMB/s  
….

Raid level 4: saving space with parity  
Add a single parity block - stores redundant information for that stripe of blocks

Compute parity: the xor of all of bits

Recover from parity

- Imagine the bit of the c2 in the first row is lock
- 1. Reading the other values in that row: 0,0,1
- 2. The parity bit is 0 → even number of 1’s in the row
- 3. What the missing data must be: 1.

Capacity

- The useful capacity is (n-1)

Reliability

- Raid 4 tolerates 1 disk failure and no more

Performance

- Steady state throughput
- ….

Random write performance for raid 4

- Overwrite a block + update the parity

Method 1: additive parity

- Read in all of the other data blocks in the strupe
- Xor those blocks with the new block
- Problem: the performance scales with the number of disks (for every drive, performance goes down as drives go up)

Method 2: subtractive parity

Update c2(old) → c2(new)

1. Read in the old data at c2 (c2(old) = 1) and the old parity (p(old) = 0)
2. calculate p(new): p(new) = (c2(old) xor c2(new)) xor …

Small write problem

- The parity disk can be a bottleneck
- ex) update blocks 4 and 13 marked with * (sildes)

Disk 0 and disk 1 can be accessed in parallel  
Disk 4 prevents any parallelism

Io latency in raid-4

A single read

- Equivalent to the latency of a single disk request

A single write

- Two reads and then two writes
- - data block + parity block
- - the reads and writes can happen in parallel

- total latency is about twice that of a single disk

Raid -5: rotating parity

Rotate the parity blocks across drives  
Remove the parity disk bottleneck for raid-4

Performance same as raid 4  
Capacity

- The useful capacity for a raid group is (n-1) where n is the number of disks

Reliability

- Raid 5 tolerates 1 disk failure and no more

Random read : better than raid 4

- Raid 5 can utilize all of the disks

Random write: n/4 * r mb/s

- The factor of four loss is the cost of using parity based raid

Performance and dont care about reliability raid 0  
Random io performance and reliability raid 1  
Capacity and reliability raid 5  
Sequential io and maximize capacity raid 5  
Files

There are two different aspects to implement file systems

Data structures

- What types of on disk structures are utilized by the file system to organize its data and metadata
- First file systems used simple structures like arrays or blocks or objects, more sophisticated file systems use complicated tree based structures

Access methods

- How does it map the calls made by a process as open(), read(), write() etc  
    …

Organization

Divide the disk into blocks

- Simple file systems use one block size, common block size is 4kb
- The blocks are addressed from 0 to n-1 in partition sizes of n 4-kb

Reserve data regions to store user data most of space is usually user data  
File system has to track which data block comprise a file, the size of the file, its owner etc → data structure called inode

Other space is used for the operating system

Inode table in file system  
Reserve some space for inode table

- This holds an array of on disk inodes
- Inode tables: 3 ~ 7, inode size: 256 bytes
- 4kb block can hold 16 inodes
- The file system contains 80 inodes (maximum number of files)
- Look at slides for example

Allocation structures  
This is to track whether inodes or data blocks are free or allocated  
Use bitmap, each bit indicates free(0) or in use(1)

- Data bitmap: for data in data region
- Other bitmap….

Superblock  
Super block contains this information for particular file system

- Ex the number of inodes, begin location of inode table etc
    
- Thus when mounting a file system, os will read the superblock first, to initialize various information
    

Each inode is referred to by inode number

- By inode number, file system calculates where the inode is on the disk
- …

File organization: the inode  
Each inode is referred to by the inode number

Continued  
Disk are not byte addressable, sector addressable  
Disk consist of a large number of addressable sectors (512 bytes)

- ex) fetch the block of inode (inode number: 32)
- Sector address iaddr of the inode block
- Blk: (inumber *sizeof(inode)) / blocksize
- Sector: (blk * blocksize) + inodeStratAddr) / sectorsize

Inode hs all of the information about a file

- File type
- Size, the number of blocks allocated to it
- Protection information
- Time information
- Etc

Inode  
First 3 numbers are owners  
Second three is group  
Last 3 everyone

….

Multilevel index

Double direct pointer - piots to a block that contains indirect blocks  
…

Continued  
Most files are small - roughly 2k is the most common size  
Average file size is growing - almost 200k is the average  
Most bytes are store in large files - a few big files use most of the space  
File systems contains lots of files - almost 100k on average  
File systems are roughly half full - even as disks grow, file systems remain -50% full  
Directories are typically small - many have few entries; most have 20 or fewer

Directory organiaztion

Directory contains a list of (entry name, inode number) pairs  
Each directory has two extra files “.” for the current directory and “..” for the parent directory

- For example, dir has three files (foo, bar, foobar)
- Look at slides for example

Free space management

- File system track which inode and data block are free or not
- In order to manage free space, we have two simple bitmaps
- When file is newly created, it allocated inode by searching the inode bitmap and update on disk bitmap
- Pre Allocation policy is commonly used….

Access paths: reading a file from disk

Issue an open(“/foo/bar”, o_rdonly)

- Traverse the pathname and thus locate the desired inode
- Begin at the root of the file system (/)
- In most unix file system, the root inode number is 2
- File stems reads in the block that contains inode number 2
- Look inside of it to find pointer to data blocks (contents of the root)
- Continues ……

Unix operating system

The good thing

- Simple and supports the basic abstractions
- Easy to use file system

Bad thing

- Terrible performance

Problem of unix operating system  
Unix file system treated disk as a random access memory

- Example of random access blocks with four file
- Look at slides

Crash consistency  
Unlike most datastructues, file system data structuters must perisit

- The must survive over the long gaul, stored on devices that retain data despite powerloss

Detailed example  
Workload

- Append of a single data block(4kb) to an existing file
- open() -> lseek() → write() → close()
- Look at diagram on slides

To achieve the transition the system perform three separate writes to the disk

- One each of inode i[v2]
- Data bitmap B[2v]
- Datablock (db)

Crash scenarios  
Imagine only a single write succeeds; there are thus three possible outcomes

1. Just the data block is written to disk

- The data is on disk, but there is no inode
- Thus it as if the write never occurred
- This case is not a problem

2. Just the upload inode (i[v2]) is written to disk

- The inode points…..

3. Just the updated bitmap is written to the disk

- The bitmap indicates that block 5 is allocated
- But there is no inode that points to it
- Thus the family system is inconsistent again

Log structured file system

When writing to disk, lfs first buffers all updates (including metadata) in an in memory segment  
When the segment is full it is written to disk in one long sequential transfer  
Lfs never overwrites existing data instead always writes segments to free locations  
Because segments are large the disk is used efficiently, and performance of family system approaches best case performance

Each write to disk has fixed overhead os positioning

Time to write out D mb

Twrite = Tposition + D/Rpeak

Tposition:positioning time, Rpeak:disk transfer rate

Go back to slides