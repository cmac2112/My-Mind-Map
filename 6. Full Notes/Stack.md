[[Memory]]

The stack is the memory set aside as scratch space for a thread of execution. 

When a funtion is called, a block is reserved on the top of the stack for local variables. When the [[Functions]] return, the block becomes unused and can be used the next time a function is called 

The stack is always reserved in a LIFO order, the most recently reserved block is always the next block to be freed.

Stack overflow can happen when too much of the stack is used

Data created on the stack can be used without pointers

You would use the stack if you know  exactly how much data you need to allocate before compule time and its not too big