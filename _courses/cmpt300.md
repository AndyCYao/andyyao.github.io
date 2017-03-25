---
layout: default
title: "Operating Systems"
code: "CMPT 300"
semester: "Winter 2017"

---

## CMPT 300 Operating Systems Winter 2017

### Master Boot Record (MBR)
The MBR stores the details of the various partitions, their start address, end addresses etc. 

It is loaded when the computer is booted, and the BIOS starts the MBR, which finds the active partition to load the operating system. 

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

#### Page Table 
Page table keeps bit flags such as isPresent, isDirty, isReadOnly etc. these flags provide the decision for page fault. 

#### Hiearchicial Page Table 
This is a lay out of page table in an effort to save space. 

Outer Page or Top Page Table is the page table directory. The outer page acts as a pointer to the inner table, 
the Internal page table is only for valid virtual memory region. The total number of virtual addresses are still the same as compare to the flat tables. However, the various internal tables are only allocated when needed. in this way it saves space. 

Multi Level PT Trade off 
-Adding more internal layers offers smaller granuarity of coverage in terms of addresses 
however, the trade off is there is more latency in accessing data. 

##### Translation Look Aside Buffer
The TLB is a MMU level address translation cache, it is used to speed up looking through page table. It stores some page table record. MMU looks to the TLB before looking at page table (which is stored in memory)

### Segmentation 
Is logical addresses that are arranged arbitrarily, could be arranged due to code, heap data, stack, etc. 

the logical address has the form 
	<segment-number, offset>
and uses the segment table to translate from logical to physical address

### Demand Paging
Note physical memory is less than virtual memory. 

## Assignment 3 , Dissect 'A comparison of software and hardware technique for x86 virtualization - Keith Adams, Ole Agesen'

### Terminologies
- X86 - refers to intel processor architecture used in PC. started as 16 bit instruction for 16 bit processor.
- hypervisor or Virtual machine monitor is a software, firmware, or hardware that runs virtual machines. 
- trap and emulate virtualization - when an OS is running as a vritual machine, some of its instruction may conflict with the host operation system. so the 'hypervisor' emulates the effect of the specific instruction or action without carrying it out. 


### Introduction
In 2006 AMD and Intel introduced hardware VMM, but this paper find it is actually not as good as before, which was software assisted VMM (that does binary translation). The author believes it is due to high VMM / Guest transition cost and rigid programming model. 

This paper will look into the reason, and explore page table updates, context switches, and I/O 

Even the recent 32 and 64 bit protected mode are not classically virtualizable (due to lack of traps when privileged instructions run at user level, and visibility of privileged state)

### Classical Virtualization
To be considered as Virtual Machine Monitor. there are three characteristics. 
- *Fidelity* Software on the VMM executes identically to its execution on hardware, save timing effect. 
- *Performance* the majority of the guest instructions are executed by the hardware w/o intervietion of VMM 
- *Safety* The VMM manages all hardware resouces

#### De-privileging 
a classical VMM executes guest operating systems directly, but at reduced privilege level. The VMM traps instruction from the de-privileged guest. 

#### Tracing Example:
VMM has a 'shadow page table' to protect the host from guest's memory access 

'Trace' refers to identifying the guest's page table and host's page table. the shadow page table is write protected. This means there is overhead involved. 

#### Simple Binary Translation 
Uses a interpreter to separate virtual state from physicial state. this prevents leakage of privileged state from physical CPU into guest. 

#### Dynamic Binary Translation
