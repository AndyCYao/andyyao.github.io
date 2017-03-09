---
layout: default
title: "Operating Systems"
code: "CMPT 300"
semester: "Winter 2017"

---

## CMPT 300 Operating Systems Winter 2017

### Memory Management
there is a distinction between virtual memory , and physical memory.
Processes do not access physical memory directly, they access virtual memory, and there is a memory management unit MMU that connects the virtual address to physical addresses.

There are two approach to connect virtual and physical memory, Page Base memory management, and segment based memory management. Page base is the dominant form of memory management and what we study. 

#### MMU memory management unit
every CPU has a MMU, and the MMU is responsible for translating the virtual memory and physical address.
it is also responsible for reporting faults, such as illegal access etc. 

a MMU also has a translation lookaside buffer, which is a cache that stores some information for faster look up. 

### Registers
The hardware has designated registers for address translation. Which are pointers to the page table, it has information about the base, the limit size, and number of segments etc. 

### Page base memory management 
A page table is a component of page base memory managment , it's like a map that connects the virtual memory to the physical memory. The table stores the virtual page number, and goes through an offset, to create the physical frame number. 

When there is a new virtual memory being accessed, there is nothing in the page table. The page table arranges for a free physical frame to be used.  

The page table is created per every process. the OS has to perform context switch to switch out the different page tables in the register. 

