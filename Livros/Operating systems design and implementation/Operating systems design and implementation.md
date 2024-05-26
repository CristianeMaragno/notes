

Computer software can be divided roughly into two kinds: system programs, which manage the operation of the computer itself, and application programs, which perform the actual work the user wants. The most fundamental system program is the operating system, whose job is to control all the computer's resources and provide a base upon which the application programs can be written. Operating systems are the topic of this book. 

  

A modern computer system consists of one or more processors, some main memory, disks, printers, a keyboard, a display, network interfaces, and other input/output devices. All in all, a complex system. Writing programs that keep track of all these components and use them

correctly, let alone optimally, is an extremely difficult job. If every programmer had to be concerned with how disk drives work, and with all the dozens of things that could go wrong when reading a disk block, it is unlikely that many programs could be written at all.

  

Many years ago it became abundantly clear that some way had to be found to shield programmers from the complexity of the hardware. The way that has evolved gradually is to put a layer of software on top of the bare hardware, to manage all parts of the system, and present the user with an interface or virtual machine that is easier to understand and program. This

layer of software is the operating system.

  

![](https://lh5.googleusercontent.com/f7ncMJNIvxtM7eCOalFA476muNKc51pQ_HUm6nfV0TKEMfCxkFpX4vKNWqQpK99L9zokvJBH6RtifvJJYTDvMwPeaxENO62zpslqCHoVxxvNHgMcKvcO6sbexU7RqhtxUlv3y7oLG8LJ-DmR4UwE)

  

The lowest level contains physical devices, consisting of integrated circuit chips, wires, power supplies, cathode ray

tubes. 

Next comes the microarchitecture level, in which the physical devices are grouped together to form functional units. Typically this level contains some registers internal to the CPU (Central Processing Unit) and a data path containing an arithmetic logic unit. On some machines, the operation of the data path is controlled by software, called the microprogram. On other machines, it is controlled directly by hardware circuits.

  

The purpose of the data path is to execute some set of instructions. Some of these can be carried out in one data path cycle; others may require multiple data path cycles. These instructions may use registers or other hardware facilities. Together, the hardware and instructions visible to an assembly language programmer form the ISA (Instruction Set Architecture) This level is often

called machine language.

The machine language typically has between 50 and 300 instructions, mostly for moving data

around the machine, doing arithmetic, and comparing values. In this level, the input/output devices are controlled by loading values into special device registers. For example, a disk can be

commanded to read by loading the values of the disk address, main memory address, byte count, and direction (read or write) into its registers. 

  

On top of the operating system is the rest of the system software. Here we find the command interpreter (shell), window systems, compilers, editors, and similar application-independent programs. It is important to realize that these programs are definitely not part of the operating

system.

  

Finally, above the system programs come the application programs. These programs are purchased (or written by) the users to solve their particular problems, such as word processing, spreadsheets, engineering calculations, or storing information in a database.

  

In this view, the function of the operating system is to present the user with the equivalent of an

extended machine or virtual machine that is easier to program than the underlying hardware.

An alternative, bottom-up, view holds that the operating system is there to

manage all the pieces of a complex system. The job of the operating system is to provide for an orderly and controlled

allocation of the processors, memories, and I/O devices among the various programs competing

for them.  In short, this view of the operating system holds that

its primary task is to keep track of who is using which resource, to grant resource requests, to account for usage, and to mediate conflicting requests from different programs and users.

  

Resource management includes multiplexing (sharing) resources in two ways: in time and in space. When a resource is time multiplexed, different programs or users take turns using it. First

one of them gets to use the resource, then another, and so on. 

The other kind of multiplexing is space multiplexing. Instead of the customers taking turns, each

one gets part of the resource. For example, main memory is normally divided up among several running programs, so each one can be resident at the same time (for example, in order to take

turns using the CPU).

  

History of Operating System

  

The first ones used mechanical relays but were very slow, with cycle times measured in seconds. Relays were later replaced by vacuum tubes. These machines were

enormous, filling up entire rooms with tens of thousands of vacuum tubes, but they were still millions of times slower than even the cheapest personal computers available today.

In these early days, a single group of people designed, built, programmed, operated, and maintained each machine. All programming was done in absolute machine language, often by wiring up plugboards to control the machine's basic functions.

  

By the early 1950s, the routine had improved somewhat with the introduction of punched cards. It was now possible to write programs on cards and read them in instead of using plugboards; otherwise, the procedure was the same.

  

The introduction of the transistor in the mid-1950s changed the picture radically. Computers became reliable enough that they could be manufactured and sold to paying customers

These machines, now called mainframes, were locked away in specially airconditioned computer rooms, with staffs of specially-trained professional operators to run them. Only big corporations or major government agencies or universities could afford their multimillion dollar price tags. To

run a job (i.e., a program or set of programs), a programmer would first write the program on paper (in FORTRAN or possibly even in assembly language), then punch it on cards. He would then bring the card deck down to the input room and hand it to one of the operators and go drink coffee until the output was ready.

  

people quickly looked for ways to

reduce the wasted time. The solution generally adopted was the batch system. The idea behind it was to collect a tray full of jobs in the input room and then read them onto a magnetic tape using a small (relatively) inexpensive computer, such as the IBM 1401, which was very good at

reading cards, copying tapes, and printing output, but not at all good at numerical calculations. Other, much more expensive machines, such as the IBM 7094, were used for the real computing.

  

The operator then loaded a special

program (the ancestor of today's operating system), which read the first job from tape and ran it. The output was written onto a second tape, instead of being printed.

  

OS/360 and the similar third-generation operating systems produced by other computer manufacturers actually satisfied most of their customers reasonably well. They also popularized several key techniques absent in second-generation

operating systems. Probably the most important of these was multiprogramming. On the 7094, when the current job paused to wait for a tape or other I/O operation to complete, the CPU simply sat idle until the I/O finished. With heavily CPU-bound scientific calculations, I/O is infrequent, so this wasted time is not significant. With commercial data processing, the I/O wait

time can often be 80 or 90 percent of the total time, so something had to be done to avoid having the (expensive) CPU be idle so much.

The solution that evolved was to partition memory into several pieces, with a different job in each partition, as shown in Fig. 1-4. While one job was waiting for I/O to complete, another job could be using the CPU. 

  

Another major feature present in third-generation operating systems was the ability to read jobs from cards onto the disk as soon as they were brought to the computer room. Then, whenever a

running job finished, the operating system could load a new job from the disk into the now-empty partition and run it. 

  

With the development of LSI (Large Scale Integration) circuits, chips containing thousands of transistors on a square centimeter of silicon, the age of the microprocessor-based personal

computer dawned. 

CP/M, MS-DOS, and the Apple DOS were all command-line systems: users typed commands at

the keyboard. Years earlier, Doug Engelbart at Stanford Research Institute had invented the GUI (Graphical User Interface), pronounced "gooey," complete with windows, icons, menus, and

mouse. 

  

The interface between the operating system and the user programs is defined by the set of "extended instructions" that the operating system provides. These extended instructions have been traditionally known as system calls, although they can be implemented in several ways. 

  

The MINIX 3 system calls fall roughly in two broad categories: those dealing with processes and those dealing with the file system.

  

Processes

  

A key concept in MINIX 3, and in all operating systems, is the process. A process is basically a program in execution. Associated with each process is its address space, a list of memory

locations from some minimum (usually 0) to some maximum, which the process can read and write. The address space contains the executable program, the program's data, and its stack.

Also associated with each process is some set of registers, including the program counter, stack pointer, and other hardware registers, and all the other information needed to run the program.

  

Periodically, the operating system decides to stop running one process and start running another, for example, because the first one has had more than its share of CPU time in the past second.

When a process is suspended temporarily like this, it must later be restarted in exactly the same state it had when it was stopped. This means that all information about the process must be explicitly saved somewhere during the suspension. For example, the process may have several

files open for reading at once. Associated with each of these files is a pointer giving the current position (i.e., the number of the byte or record to be read next). When a process is temporarily suspended, all these pointers must be saved so that a read call executed after the process is restarted will read the proper data. 

  

If a process can create one or more other processes (usually referred to as child processes) and these processes in turn can create child processes, we quickly arrive at the process tree structure of Fig. 1-5. Related processes that are cooperating to get some job done often need to communicate with one another and synchronize their activities. This communication is called interprocess communication.

  

![](https://lh6.googleusercontent.com/yrmY6qXNMAu0plDFX-gFxKz0MbN9Fb1r0AoHk1Iy3MlSlh60HDskf-BhDxBT343vrjfdJGCYDuCKpgvh2hgEkwKLxTS4qzgPWMOGzKQX5udCNCVi6C3y2mCda6qscf7WjAiAd7rfldEecEDeYsQj)

  

Other process system calls are available to request more memory (or release unused memory), wait for a child process to terminate, and overlay its program with a different one.

  

Occasionally, there is a need to convey information to a running process that is not sitting around waiting for it. For example, a process that is communicating with another process on a different computer does so by sending messages to the remote process over a network. To guard against the possibility that a message or its reply is lost, the sender may request that its own operating system notify it after a specified number of seconds, so that it can retransmit the message if no acknowledgement has been received yet. After setting this timer, the program may continue doing other work.

  

Each person authorized to use a MINIX 3 system is assigned a UID (User IDentification) by the system administrator. Every process started has the UID of the person who started it. A child process has the same UID as its parent. Users can be members of groups, each of which has a

GID (Group IDentification). One UID, called the superuser (in UNIX), has special power and may violate many of the

protection rules. 

  

Files

The other broad category of system calls relates to the file system. System

calls are obviously needed to create files, remove files, read files, and write files. Before a file can be read, it must be opened, and after it has been read it should be closed, so calls are provided to

do these things.

  

![](https://lh5.googleusercontent.com/MtDCm1UJu2s6oM1Mc3pDgJ0dCbwhIWj6gc956zVEFXdYcJJwyee7V2w7Cstz5dWaduKMluQmhzQKyPF7pTBo7kLMpD2jL7WAbGUFDQOzW7HHufUvUletFNprrF8WiBKzCAvo26a5tgZ6pNBOxB4N)

  

The process and file hierarchies both are organized as trees, but the similarity stops there. Process hierarchies usually are not very deep (more than three levels is unusual), whereas file hierarchies are commonly four, five, or even more levels deep. Process hierarchies are typically

short-lived, generally a few minutes at most, whereas the directory hierarchy may exist for years.

  

Files and directories in MINIX 3 are protected by assigning each one an 11-bit binary protection code. The protection code consists of three 3-bit fields: one for the owner, one for other members

of the owner's group (users are divided into groups by the system administrator), one for everyone else, and 2 bits we will discuss later. Each field has a bit for read access, a bit for write access, and a bit for execute access. These 3 bits are known as the rwx bits. For example, the

protection code rwxr-x--x means that the owner can read, write, or execute the file, other group members can read or execute (but not write) the file, and everyone else can execute (but not read or write) the file. For a directory (as opposed to a file), x indicates search permission. A dash means that the corresponding permission is absent (the bit is zero).

**