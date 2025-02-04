
Chapter 1
---
 The book tells that today's operating system is complex and for understanding them we should use "abstraction".  
  
The OS could be divide into different layers for abstraction.  
  
- Userspace  
This is the userland where the process of users are initiated. This layer could as well divided into multiple layers.Where higher layers are for user interaction and lower layer are simple programs which does one task only libraries or binaries.  
  
- Kernel  
Then comes the kernel which is used to manage hardware and for safety of the system. Kernel also helps in memory management, process management, Device Drivers and system calls.  
For system Calls There is 2 main term :  
* fork() => which just copies the current process or memory state.  
* exec() => it just loads the binaries into the memory for processing.  

The kernel is responsible for context switching. To understand how this
works, let’s think about a situation in which a process is running in user
mode but its time slice is up. Here’s what happens:
1. The CPU (the actual hardware) interrupts the current process based on
an internal timer, switches into kernel mode, and hands control back to
the kernel.
2. The kernel records the current state of the CPU and memory, which
will be essential to resuming the process that was just interrupted.
3. The kernel performs any tasks that might have come up during the
preceding time slice (such as collecting data from input and output, or
I/O, operations).
4. The kernel is now ready to let another process run. The kernel analyzes
the list of processes that are ready to run and chooses one.
5. The kernel prepares the memory for this new process and then pre-
pares the CPU.
6. The kernel tells the CPU how long the time slice for the new process
will last.
7. The kernel switches the CPU into user mode and hands control of the
CPU to the process.
  
  
- Hardware  
At last comes the hardware devices.  
I thought CPU was the chief hardware of the computer system and memory is auxiallary to chief and helps for operation. But according to the book the main chief role is played by the memory and auxiallary role is played by the CPU for operation.  
Memory state is the orientation of the current bits/data active in the memory.  
Kernel has its own private space and users have its own private space.  
  
  
Even root has its own space in user space. It does not run in kernel space.