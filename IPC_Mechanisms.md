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

## 2.Why we use IPC Mechanism? 
We use IPC mechanisms to allow different processes to communicate and share data with each other, because processes cannot directly access each other’s memory.

In simple points:

To share data between processes

To send messages between processes

To synchronize processes

To coordinate work between processes

To avoid conflicts when using shared resources

## 3 What are the types of IPC Mechanism's? 
1. Pipes

Pipes are used for one-way communication between related processes (like parent and child).

Data flows in a single direction, just like water in a pipe.

2. Named Pipes (FIFOs)

Named pipes are similar to normal pipes but have a name in the file system.
They allow communication between unrelated processes also.

3. Message Queues

A message queue works like a message box where one process sends messages and another process reads them.

It is useful for exchanging structured messages.

4. Semaphores

Semaphores are used for synchronization, not data transfer.

They act like signals (wait / go) to control access to shared resources and avoid conflicts.

5. Shared Memory

Shared memory allows two or more processes to share the same memory area.

It is the fastest IPC mechanism because data does not need to be copied.

## 4.What is meant by “unicast” and “multicast” IPC?
Unicast IPC

Unicast IPC means communication between one sender and one receiver (1-to-1).

Example:

One process sends data → Only one specific process receives it.

Multicast IPC

Multicast IPC means communication from one sender to multiple receivers at the same time (1-to-many).

Example:

One process sends data → Many processes receive it together.
## 5.What is meant by PIPES? 
Pipes are unidirectional IPC mechanisms used for communication between two related processes (like parent and child).

They allow data to flow in one direction only, just like water in a pipe.

## 6.. What is meant by Blocking Calls?
A blocking call is a function call where the process waits (or blocks) until the operation is completed. The process cannot do anything else during this waiting time.

Simple example:

If a process calls read() and there is no data, it waits until data arrives → this is a blocking call.

## 7.What are the types of Blocking Calls?
Types of Blocking Calls

## Read Blocking Call

The process waits until data is available to read.

Example: read() from a pipe or file.

## Write Blocking Call

The process waits until there is space in the buffer to write data.

Example: write() to a full pipe or socket.

## Accept Blocking Call (Sockets)

Server waits until a client tries to connect.

Example: accept() function in a TCP server.

## Connect Blocking Call (Sockets)

Client waits until it connects to the server.

Example: connect() function in a TCP client.

## 8 What are the different types of I/O Calls?
I/O calls are how a process communicates with input/output devices (like keyboard, screen, files, network).

They can be classified into two main types:
### 1 Blocking I/O (Synchronous I/O)

The process waits until the I/O operation is complete.

Example: read() or write() on a file or socket.

During this time, the process cannot do anything else.

### 2. Non-Blocking I/O (Asynchronous I/O)

The process does not wait; it continues executing while the I/O operation happens in the background.

Example: read() on a non-blocking socket.

The process can check later if the operation is complete.

** Buffered I/O – Data is temporarily stored in a buffer before reading/writing.

** Direct I/O – Data goes directly between process and device without buffering.

## 9.What are the I/O calls we are used in IPC Mechanisms? 

| **IPC Mechanism**       | **I/O Calls**                            | **Purpose**                                      |
| ----------------------- | ---------------------------------------- | ------------------------------------------------ |
| **Pipes / Named Pipes** | `read()`, `write()`, `open()`, `close()` | To read/write data and open/close the pipe       |
| **Message Queues**      | `msgsnd()`, `msgrcv()`                   | To send and receive messages                     |
| **Shared Memory**       | `shmget()`, `shmat()`, `shmdt()`         | To create/get shared memory, attach, detach it   |
| **Semaphores**          | `semop()`                                | To perform semaphore operations (like wait/post) |

## 10 What are the Blocking Calls used in IPC?
Blocking Calls Used in IPC

Blocking calls are those where a process waits until the operation is complete. In IPC, the common blocking calls are:

read()

Waits until data is available to read from a pipe, message queue, or shared memory.

write()

Waits until space is available in the buffer to write data.

msgsnd()

Waits if the message queue is full before sending a message.

msgrcv()

Waits if the message queue is empty before receiving a message.

semop()

Waits if a semaphore condition is not satisfied (used for synchronization).

shmat() (sometimes blocking)

Waits while attaching a shared memory segment if required resources are not available.

## 11.

