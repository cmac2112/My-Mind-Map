[[operating systems]] [[Operating System]]

Multi Level Feedback Queue (mlfq)

- General purpose scheduler that learns from the past to predict the future
- Must support two job types with distinct goals  
    – ‘interactive’ programs care about response time  
    – ‘batch’ programs care about turnaround time

Rules and priorities  
Mlfq has a distinct number of queues

- Each queue is assigned a different priority queue

A job that is ready to run is on a single queue

- A job on a higher queue is chosen to run
- Use round robin scheduling almost jobs in the same queue

Ex:  
Q3: -> a  
Q2: -> b  
Q1:  
Q0: ->c->d

(Rule 1: if priority(a) > priority (b), a runs b doesn't)  
(Rule 2: if priority(a) = priority (b), a & b run in RR)

How to change priority:

- New rules

– Rule 3: when a job enters the system, it is placed at the highest priority  
– Rule 4a: if a job uses up an entire time slice while running, its priority is reduced  
– Rule 4b: if a job gives up the cpu before the time slice is up, it stays at the same priority level  
– Rule 5: after some time period S, move all jobs in the system to the topmost queue

These rules do not account for gaming the system

- How do we prevent the gaming of our scheduler?

– better accounting of cpu time at leave  
– rewrite rules 4a and 4b into Rule 4: once a job uses up its time allotment at its given level (regardless of how many time it has given up the cpu) its priority is reduced.

Proportional share schedudler  
Fair share scheduler

- Guarantee that each job obtains a certain percentage of cpu time
- Not optimized for a turnaround or response time

Example is a lottery schedule

Lottery schedule:

- Tickets

1. Represents the share of a resource that a process should have
2. The percent of tickets represents its share of the system resource in question

- The scheduler picks a winning ticket.

1. Load the state of that winning process and runs it.

Ticket currency

- A user allocates tickets among their own jobs in whatever currency they would like
- The system converts the currency into the correct global value

Ticket Transfer

- A process can temporarily hand off its tickets to another process

Ticket inflation

- A process can temporarily raise of lower the number of tickets it owns
- If any one process needs more cpu time, it can boost its tickets

Example: There are three processes A,B,C

- Keep processes in a list
- If winning ticket is 110 who wins/runs?  
    Head → job a(100) → …

Unfairness metric (u)

- The time the first job completes divided by the time that the second job completes

ex)  
There are two jobs each job has runtime 10

- First job finishes at time 10
- Second job finishes at time 20

Logarithmic

Problems

- How to assign tickets
- - one problem we have not addressed

Why not deterministic

- Why use randomness at all
- Randomness is simply (and approximately correct) but occasionally will not deliver the right proportions

Stride scheduling was born for these reasons

Stride scheduler

- Deterministic fair share scheduler
- Stride of each processes
- - a large number / the number of tickets of the process
- -ex) a large number = 10000
- – process a has 100 → stride of a is 100
- – process b has 50 → stride of b is 200

A process runs increment a counter (=pass value) for its by its stride

- Pick the process to run that has the lowest pass value

Linux completely fair scheduler (cfs)

- Fair share scheduler in a highly efficient and scalable manner
- Aims to spend very little time making scheduling decisions
- Inherent design
- Clever use of data structures

Fairly divides the cpu evenly among competing processes

- Simple counting based …

If it switches to often, fairness is increased but overhead is high  
If it switches less often, overhead is minimized, but short term fairness is decreased

- Scheduled latency

Cfs uses this value to determine how long process should run  
Cfs divides this number by number of processes running to determine how long time slice is  
What if there are too many processes?

- Minimum granularity

Cfs will never set the time slice to less than this value

Cfs also enables controls over process priority

- Allows admins to give some processes higher share than other

Unix nice can be set between -20 and 19  
Cfs maps the nice value to a weight.

Time slice = wight/weight *schedule latency

ex) A = 5, b = 0

3121/1024+3121 * 48 = 36ms

1024/ 1024+3121 = ¼ *48 = 12ms