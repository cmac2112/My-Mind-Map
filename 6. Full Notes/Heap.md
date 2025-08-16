[[Memory]]

The heap is memory set aside for dynamic allocation. Unlike the stack there is no enforced pattern to the allocation and deallocation of blocks from the heap; you can allocate a block at any tiome and free it at any time. 

variables on the heap must be destroyed manually and never fall out of scope.
in [[C]] data created on the heap will be pointed to by pointers and allocated with`new` or `malloc` respectively
