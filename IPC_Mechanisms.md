## 1 What is meant by an IPC Mechanism?
IPC (Inter-Process Communication) mechanism is a method used to share data and communicate between two or more processes. Since processes cannot directly access each other’s memory, IPC provides safe ways for them to exchange information

Different Types of IPC Mechanisms

1. Pipes

Pipes are used for one-way communication between related processes (like parent and child).

Data flows in a single direction, like water in a pipe.

2. Named Pipes (FIFOs)

Named pipes work similar to normal pipes but have a name in the file system.

They allow communication between unrelated processes also.

3. Message Queues

A message queue is a message box where one process sends messages and another process reads them.

Useful when processes need to exchange structured messages.

4. Semaphores

Semaphores are used for synchronization, not data transfer.

They act like signals (wait / go) to control access to shared resources and avoid conflicts.

5. Shared Memory

Shared memory allows two or more processes to share the same memory area.

It is the fastest IPC mechanism because data does not need to be copied.

## 2.
