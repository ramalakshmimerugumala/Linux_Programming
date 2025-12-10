## 1 What is memory management in system programming?
It is the process of giving memory to programs and taking it back when they are done.

## Why we need it?

To avoid memory waste

To run many programs at the same time

To stop programs from using other program’s memory

To prevent crashes

## Parts of Program Memory

Text → program code

Data → global/static variables

Stack → function calls & local variables

Heap → dynamic memory (malloc/free)

Memory management = Allocate memory + Use memory + Free memory safely

## 2.Define virtual memory
Virtual memory is a technique that uses both RAM and hard disk together so that a system can run large programs even if RAM is not enough.

When RAM becomes full → system moves some data to hard disk

This extra space on hard disk acts like fake RAM

This helps the system run smoothly without crashing

## 3 Differentiate between physical memory and virtual memory
| **Physical Memory**            | **Virtual Memory**                 |
| ------------------------------ | ---------------------------------- |
| Actual RAM inside the computer | Combination of RAM + hard disk     |
| Limited and fixed              | Can be larger than RAM             |
| Faster                         | Slower (because it uses hard disk) |
| Stores data currently in use   | Stores extra data when RAM is full |
| Managed directly by hardware   | Managed by OS using paging         |

Physical memory = real RAM.
Virtual memory = extra fake RAM created using hard disk.

## 4.What is the role of an operating system in memory management?
Role of Operating System in Memory Management

Allocates memory to programs

Keeps track of which program uses which memory

Protects memory so programs don’t access each other’s space

Uses virtual memory when RAM is full

Frees memory when a program finishes

## 5.Explain the purpose of memory allocation.
Purpose of Memory Allocation

To give space for a program to store data and variables

To make sure memory is used properly without wastage

To allow multiple programs to run at the same time

To prevent one program from using another program’s memory

To improve system speed and performance

## 6 Describe the significance of memory deallocation.
Significance of Memory Deallocation

Frees the memory that a program no longer needs

Prevents memory leaks

Makes memory available for other programs

Improves system performance

Avoids system slowdown or crashes.

## 7.Define fragmentation in memory management
Fragmentation is the condition where memory gets broken into small unused pieces, making it hard to allocate large blocks of memory

## 8 What are the types of fragmentation?
1️ Internal Fragmentation

Happens when allocated memory is more than required

Extra space inside the block is wasted

Example: You request 30 bytes, OS gives 40 bytes → 10 bytes wasted.

2️ External Fragmentation

Free memory is available but in small scattered pieces

Cannot give a big block even though total free space is enough.

Example: Free spaces like 10B + 5B + 7B + 3B (not continuous)

## 9.Explain internal fragmentation
Internal fragmentation happens when the memory given to a program is more than what it actually needs, and the extra space inside that block is wasted

Internal fragmentation = wasted space inside an allocated memory block.
## 10.Explain external fragmentation
External fragmentation happens when free memory exists but it is divided into many small scattered pieces, so a large block cannot be allocated even though total free space is enough

Example

Free spaces in memory:
8 KB + 6 KB + 4 KB + 5 KB (all separated)

If a program needs 20 KB, OS cannot give it,
because memory is not continuous.
External fragmentation = free memory is available but scattered, not continuous.

## 11.How is fragmentation managed in memory allocation?
## Compaction

OS moves memory blocks together

Makes all free space continuous

## Paging

Breaks memory into fixed-size pages

No external fragmentation

## Segmentation with Paging

Segments → logical divisions

Pages → avoid fragmentation inside segments

## Best-fit / First-fit / Worst-fit

Choose the right free block to reduce wastage

## 12 Describe the concept of paging.
Paging splits logical (virtual) memory and physical memory into equal-sized blocks so pages can be placed in any free frame — this removes external fragmentation.

Page = fixed-size block in virtual memory.

Frame = same-size block in physical RAM.

Page table = map from page number → frame number.

Page size = common sizes: 4 KB (4096 bytes), 8 KB, etc.

## 1️ Page Table

Virtual memory is divided into equal-sized pages → called virtual pages

Physical memory (RAM) is divided into frames of the same size

Pages can go in any free frame → no need for contiguous memory

Page table keeps track of which page is in which frame

Advantage: avoids external fragmentation

## 2️ Address Split

Each virtual address = Page Number + Offset

Page Number: which page in virtual memory

Offset: exact location inside that page

Example:

Page size = 4 KB = 4096 bytes → offset = 12 bits

32-bit virtual address → page number = 32 − 12 = 20 bits

[ 20-bit Page Number | 12-bit Offset ]


Page number → used to look in page table

Offset → exact byte inside the page/frame

## 3️ Address Translation
Step-by-step:

CPU gets virtual address

Splits it → page number + offset

Looks in page table → finds frame number

Combines frame start address + offset → physical address

Page Fault:

If page not in RAM → OS loads it from disk → updates page table → CPU retries instruction

Example:

Virtual address = 20000

Page size = 4096 → offset = 20000 % 4096 = 3616

Page number = 20000 ÷ 4096 = 4

Page table → page 4 in frame 10

Physical address = frame start + offset = 10×4096 + 3616 = 44576
## 13 Explain segmentation.
Memory is divided into logical parts called segments

Example: code, data, stack, heap

Each segment = base address + size (limit)

Virtual address = segment number + offset

OS uses a segment table to map segments → physical memory

Advantages: matches programmer view, allows protection/sharing

Disadvantages: can cause external fragmentation

## 14  What is the difference between paging and segmentation?
| **Paging**                                 | **Segmentation**                               |
| ------------------------------------------ | ---------------------------------------------- |
| Memory divided into **fixed-size pages**   | Memory divided into **variable-size segments** |
| Avoids **external fragmentation**          | Can have **external fragmentation**            |
| Page size is fixed                         | Segment size is variable                       |
| Logical address = **page number + offset** | Logical address = **segment number + offset**  |
| Easy to manage                             | Matches programmer’s logical view              |
| No protection by default                   | Segments can have **protection/sharing**       |

## 15  Define page table
Page table is a data structure used by the OS to map virtual pages → physical frames.

Keeps track of:

Which frame a page is in

Whether the page is in RAM or not

Access rights (read/write/execute)

## 16 Define Memory Management Unit (MMU)
The MMU is a hardware unit in the CPU that converts virtual addresses into physical addresses using the page table

MMU = hardware that does address translation automatically.

What it does:

Reads virtual address

Looks up page table

Finds the physical frame

Gives physical address to RAM

## 17 Explain the role of MMU in memory management.
1️ Converts Virtual Address → Physical Address

CPU gives virtual address

MMU uses page table and converts it to physical address

This is called address translation

2️ Protects Memory

Stops one process from accessing another process’s memory

Uses access rights (read/write/execute)

3️ Supports Paging & Segmentation

MMU handles page tables

Helps OS in paging and segmentation

4️ Generates Page Faults

If the page is not in RAM

MMU alerts OS → OS loads page from disk to RAM

## 18 Describe the translation lookaside buffer (TLB).
TLB = fast memory that stores recent address translations to speed up paging

TLB stores the most recently used address translations.

When the CPU needs a physical address, it first checks the TLB:

If the entry is found (TLB hit):

CPU gets the physical address directly and fast.

If the entry is not found (TLB miss):

MMU uses the page table to translate the address,
and then updates the TLB with this new translation.

## 19 What is TLB miss? How is it handled?
TLB miss = entry not in TLB, so MMU fetches from page table and updates TLB.

How a TLB Miss is handled? 

CPU checks TLB → entry not found → TLB miss

MMU goes to the page table in RAM

Page table gives the frame number

MMU updates the TLB with this new translation

CPU retries the instruction using the updated TLB

## 20. Discuss the working principle of MMU
1️ CPU generates a virtual address

This address has:

Page number

Offset

2️ MMU checks the TLB

If found → TLB hit → fast translation

If not found → TLB miss → go to page table

3️ MMU looks into the page table

Finds the frame number corresponding to the page number.

4️ MMU creates the physical address

Physical Address = Frame number + offset

5️ MMU checks protection

Ensures the program is allowed to read/write/execute that memory.

6️ If page not in RAM → page fault

OS loads the required page from disk → updates page table → MMU continues.

## 21 Explain the concept of address translation in MMU
Address translation means converting a **virtual address** (used by programs) into a **physical address** (used by hardware).  
The MMU does this using page tables and the TLB

## 22 How does MMU support virtual memory
MMU allows programs to use virtual addresses by:

## Mapping virtual addresses to physical addresses
(using paging and address translation)

## Using page tables and the TLB
to find frame numbers quickly.

## Enabling programs to use more memory than RAM
by storing extra pages on disk (virtual memory).

## 23  Describe the process of page table traversal in MMU
Page Table Traversal in MMU

1.MMU gets a virtual address from the CPU.

2.Checks the TLB (fast cache for recent translations).

3.If TLB miss: looks up the page table in memory.

4.Finds the corresponding physical frame.

5.Forms the physical address = frame number + offset

## 24 What is page fault handling in MMU?
Page Fault Handling in MMU

Page fault: occurs when a program tries to access a page not in RAM.

Steps to handle a page fault

MMU informs the OS about the missing page.

OS loads the page from disk (swap) into RAM.

Page table is updated with the new frame number.

CPU restarts the instruction that caused the fault

## 25  Explain the page replacement algorithms used in MMU
When RAM is full, MMU needs to remove a page to load a new one.  
**Page replacement algorithms** help decide **which page to remove**

MMU itself doesn’t choose the algorithm; the OS decides which page replacement algorithm to use.

Commonly used algorithms in real systems:

LRU (Least Recently Used) → most popular

FIFO (First-In-First-Out)

Clock (Second Chance)

Optimal algorithm is only theoretical (can’t predict future accesses).

## 26  Define page replacement algorithms
Page replacement algorithms are rules used by the operating system to decide which page to remove from RAM when memory is full and a new page needs to be loaded.

## 27 Describe the FIFO page replacement algorithm
FIFO (First-In-First-Out) removes the page that entered RAM first.

# How FIFO Works:

Pages are loaded into RAM in order.

When RAM becomes full and a new page is needed:
→ Remove the oldest page (the one that came first).

Insert the new page at the end.

 Advantages

Simple to implement — just remove the oldest page.

Low overhead — no need to track usage or timestamps.

 Disadvantages

May remove frequently used pages, causing more page faults.

Suffers from Belady’s anomaly, where more frames can still cause more faults

## 28 Discuss the optimal page replacement algorithm.
The Optimal algorithm removes the page that will not be used for the longest time in the future.

# How it works:

When a new page is needed and RAM is full:

Look at the future page requests.

Remove the page that will be used farthest in the future.

# Why it’s not used in real systems?

We cannot know the future page accesses in real time.

So it is only used for theoretical comparison, not in real OS.

## 29  Explain the LRU (Least Recently Used) page replacement algorithm.
LRU removes the page that has not been used for the longest time.

How LRU Works:

The system tracks which pages are being used.

When RAM is full and a new page is needed:

→ Remove the page that was used farthest in the past.

Insert the new page.

It is More accurate than FIFO  
Harder to implement (needs tracking of usage).

Advantages of LRU

More accurate — removes the page least likely to be used again (better than FIFO).

Reduces page faults in most real-world workloads.

 Disadvantages of LRU

Difficult to implement — requires tracking the usage order of pages.

Higher overhead — needs extra hardware or data structures (counters, stacks).

## 30 What is the clock page replacement algorithm?

Clock Page Replacement Algorithm

The Clock algorithm is an improved version of FIFO.
It gives each page a second chance before removing it.

How it Works

All pages are arranged in a circular list (like a clock).

Each page has a reference bit (0 or 1).

A hand/pointer moves like a clock hand.

Replacement Steps

If the pointer finds a page with reference bit = 0 → remove it.

If the page has reference bit = 1 →

Set it to 0 (give second chance)

Move the pointer to next page

Continue searching

Advantages (2)

More efficient than FIFO and simpler than LRU.

Gives pages a fair “second chance,” reducing unnecessary replacements.

Disadvantages (2)

Not as accurate as LRU in predicting future use.

Still needs hardware support for reference bits.

## 31.Discuss the advantages and disadvantages of each page replacement algorithm.
# 1. FIFO (First-In-First-Out)

Advantages:

Very simple to implement.

Low overhead—no need to track usage.

Disadvantages:

May remove frequently used pages.

Suffers from Belady’s anomaly (more frames → more faults sometimes).

# 2. Optimal (OPT)

Advantages:

Gives the minimum possible page faults.

Best theoretical performance.

Disadvantages:

Not practical—requires future knowledge.

Used only for comparison, not in real systems.

# 3. LRU (Least Recently Used)

Advantages:

Good performance—close to optimal.

Removes least useful page based on real usage.

Disadvantages:

Hard to implement in hardware/software.

Tracking usage adds overhead and cost.

# 4. Clock (Second Chance Algorithm)

Advantages:

Simple and efficient.

Better than FIFO — gives “second chance” to active pages.

Disadvantages:

Not as accurate as LRU.

Needs reference bit support in hardware.

## 32 Compare and contrast different page replacement algorithms.

| Algorithm                     | How it Works                                                              | Advantages                            | Disadvantages                                | Performance       |
| ----------------------------- | ------------------------------------------------------------------------- | ------------------------------------- | -------------------------------------------- | ----------------- |
| **FIFO (First-In-First-Out)** | Removes the **oldest loaded page**                                        | Simple, easy to implement             | Removes useful pages, Belady’s anomaly       | **Poor–Moderate** |
| **Optimal (OPT)**             | Removes the page that will **not be used for the longest time in future** | Minimum page faults, best theoretical | Not practical (requires future knowledge)    | **Best (Ideal)**  |
| **LRU (Least Recently Used)** | Removes the page **not used for the longest time in the past**            | Closer to optimal, good accuracy      | Hard/expensive to implement (tracking usage) | **Good**          |
| **Clock (Second Chance)**     | Similar to FIFO but **gives second chance** using reference bit           | Efficient, simple, better than FIFO   | Less accurate than LRU                       | **Moderate–Good** |

## 33 Explain the working of the NRU (Not Recently Used) page replacement algorithm.
NRU removes a page based on whether it was used recently and whether it was modified.

Every page has two bits:

R bit (Reference bit): becomes 1 when page is accessed

M bit (Modified bit): becomes 1 when page is written/updated

The OS resets the R bit regularly, so it can see which pages were used recently.
| Class | R | M | Meaning                                          |
| ----- | - | - | ------------------------------------------------ |
| **0** | 0 | 0 | Not used recently, not modified → BEST to remove |
| **1** | 0 | 1 | Not used recently, modified                      |
| **2** | 1 | 0 | Used recently, not modified                      |
| **3** | 1 | 1 | Used recently, modified → WORST to remove        |
Advantages

Simple

Faster than LRU

Reduces unnecessary disk writes

 Disadvantages

Not very accurate

Depends on when R bit is reset

## 34 Describe the working of the Second Chance page replacement algorithm.
The Second Chance algorithm is an improved version of FIFO. It gives each page a “second chance” before removing it.

How It Works 

All pages are arranged in a circular list (like a clock).

Each page has a Reference bit (R bit):

R = 1 → page was recently used

R = 0 → page not used recently

A clock hand points to the "oldest" page

## 35 Discuss the enhancements to basic page replacement algorithms.
Basic algorithms like FIFO and LRU are simple, but not always efficient. So operating systems add extra techniques to improve page replacement.

Reference & Modify bits (R & M):

Helps choose pages that are not recently used or not modified.

Aging Algorithm:

Uses counters to track page usage → removes least recently used pages.

Working Set Model:

Keeps pages used in the recent past, removes others.

Page Buffering:

Stores removed pages in a buffer → can bring them back quickly if needed.

Adaptive Algorithms:

Changes replacement strategy automatically based on workload.

## 36 Define segmentation in memory management
Segmentation divides memory into parts based on **logical sections** like:
- Code
- Data
- Stack  
Each segment can be of different size.

## 37 Explain the benefits of segmentation
Benefits of Segmentation

Logical division of program → code, data, stack, heap.

Easier to manage and protect memory → different access rights per segment.

Segments can grow/shrink independently → flexible memory use

## 38 What are the disadvantages of segmentation?
Can cause external fragmentation

Harder to manage compared to paging

Slower address translation
## 39 Describe the implementation of segmentation
Segmentation uses a segment table to map virtual addresses to physical memory safely.

## Segment Table:

Each process has a table with entries for each segment:

Base address → where the segment starts in memory

Length → size of the segment

Access rights → read/write/execute

## Address Translation:

Virtual address = Segment Number + Offset

Physical address = Base + Offset

## Protection:

If offset > segment length → error / access violation

## 40 Discuss segmentation fault and its causes.
Segmentation Fault

A segmentation fault (segfault) happens when a program accesses memory it shouldn’t.

It’s a type of runtime error

Common Causes

Accessing memory beyond segment limits

Example: accessing array out of bounds.

Dereferencing invalid pointers

Example: using a pointer that is NULL or uninitialized.

Writing to read-only memory

Example: trying to modify a string literal.

Stack overflow

Example: infinite recursion that exceeds stack size.

## 41

