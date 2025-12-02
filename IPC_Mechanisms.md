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

## 11. What is meant by Named Pipes?
Named pipes are used for communication between two processes, even if they are unrelated.

Data can flow one way or two ways.

They have a name in the file system, so any process knowing the name can use it to send or receive data.

## 12 Where is the FIFO Object created?
A FIFO (Named Pipe) object is created in the file system.

It appears as a special file.

Any process can use this file name to communicate.

Created using the system call:

mkfifo("filename", permissions);

## 13 What is the call used to create a FIFO Object? 
mkfifo("filename", permissions);

## 14 What are the Blocking Calls used in Named Pipes?
Blocking Calls Used in Named Pipes

open()

If a process tries to open a named pipe for reading, it waits (blocks) until another process opens it for writing.

read()

If there is no data in the named pipe, the process waits (blocks) until data becomes available.

## 15 Why read system calls acts as a blocking call?
When a process calls read() to read from a pipe, named pipe, or message queue, it waits until data is available.

If there is no data, the process cannot continue and stays blocked.

This is why read() is called a blocking call.
## 16 Difference between the Named Pipes and Pipes?
| Feature            | **Pipe**                                       | **Named Pipe (FIFO)**                    |
| ------------------ | ---------------------------------------------- | ---------------------------------------- |
| **Processes**      | Only **related processes** (parent-child)      | **Related or unrelated processes**       |
| **Existence**      | **Temporary**, exists only while processes run | **Permanent**, exists in **file system** |
| **Identification** | No name, identified by pipe descriptor         | Has a **name in the file system**        |
| **Direction**      | Usually **one-way**                            | Can be **one-way or two-way**            |
| **Creation**       | Using `pipe()` system call                     | Using `mkfifo()` system call             |

## 17 What is return value of read system call?
Return Value of read() System Call

The read() system call returns:

Number of bytes actually read

If data is available, it returns the count of bytes read.

0

Indicates end of file (EOF) or no more data to read.

-1

Indicates an error occurred (e.g., invalid file descriptor).
## 18 . What is meant by message queue?
A Message Queue is an IPC mechanism that allows processes to send and receive messages in a queue.

Messages are stored in first-in, first-out (FIFO) order.

Processes can send messages to the queue (msgsnd()) and receive messages from the queue (msgrcv()).

Useful when processes need to exchange structured data.
## 19 Why we use message queues? 
Message queues are used to allow processes to communicate and exchange data safely and efficiently.

Process Communication – Allows processes to send and receive messages.

Asynchronous Communication – Sender and receiver do not need to run at the same time.

Data Organization – Messages are stored in a queue (FIFO), ensuring order.

Safe Sharing – Avoids direct access to each other’s memory.

Structured Data – Can send structured messages instead of just bytes.
## 20 What is difference between Named Pipe and Message Queue? 
| Feature           | **Named Pipe (FIFO)**                             | **Message Queue**                                           |
| ----------------- | ------------------------------------------------- | ----------------------------------------------------------- |
| **Communication** | Used to **send data bytes** between processes     | Used to **send/receive structured messages**                |
| **Processes**     | Can be **related or unrelated**                   | Can be **related or unrelated**                             |
| **Persistence**   | Exists as a **file in file system**               | Exists **in kernel memory**                                 |
| **Order**         | Data flows **in order written**, no message types | Messages stored in **queue with types**, can be prioritized |
| **Blocking**      | `read()` and `write()` may block                  | `msgsnd()` and `msgrcv()` may block                         |
| **Data Handling** | Works like a **stream of bytes**                  | Works like **messages with defined structure**              |


