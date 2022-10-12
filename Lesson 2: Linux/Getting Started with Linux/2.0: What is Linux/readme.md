# A Brief History

## Bell Labs
Linux really started at Bell Labs. If you are not familiar, Bell Labs was founded by Alexander Graham Bell, the inventor of the telephone. The laboratory was generally flush with funding due to a near monopoly on telephone systems in the United States which provided a consistant and profitable revenue stream. The labs focused on technology relating to telecommunications. A few inventions related to IT and Cybersecurity are:

* 1920s - One time pad ciphers
* 1947 - The transistor
* 1947 - Hamming codes (used for error correction)
* 1948 - *A Mathematical Theory of Communication* is published (authored by Claude Shannon)
* 1949 - *Communication Theory of Secrecy Systems* is published (authored by Claude Shannon)
* 1953 - The Kaurnaugh map (named after Maurice Karnaugh)
* 1957 - Kruskal's algorithm is developed (by Robert C. Prim and Joseph Kruskal)
* 1969 - UNIX is developed by Dennis Ritchie and Ken Thompson
* 1972 - The C programming language is invented by Dennis Ritchie
* 1985 - The first commercial release of the C++ programming lanuage. Deveolpment began by Bjarne Stroupstrup in 1979 while he was working at Bell Labs

## UNIX
So what is UNIX? UNIX was an early operating system. It was written as a less complex version of a previous operatins system called MULTICS (UNIX was originally spelled UNICS). 

UNIX has a few major components:
1. A kernel - This is a hardware compatibility layer that allows code to be a lot more platform agnostic. It is part of the operating system that takes instructions like "write <number> bytes to the hard drive at location <location>" and uses them to talk to the controller on the disk to actually write the data.

2. Commands - These are small programs that do one task. The UNIX philosophy is that you should write small programs that each do one thing really well, then combine them together to do more complex things.

3. Documentation - Usage of commands are bundled together with them so you don't need to consult a physical manual.

Due to a previous lawsuit, AT&T (and Bell Labs) weren't allowed to enter the computer market. Because of this, UNIX was licenced to anyone interested which helped it to grow quickly in popularity. In 1984, AT&T sold Bell Labs, and they were then able to sell UNIX as a commercial product, which they began to do.

## The GNU Project
In 1983, while working at the MIT Artificial Intelligence Laboratory, Richard Stallman decided to begin writing an open and free operating system. He quit his job at MIT and began work in early 1984 so they could not claim ownership of his software. GNU was intended to be UNIX compatible, so components could be replaced piece by piece. 

By the early 90s, most of GNU was working, but a lot of the low level components like device drivers and the kernel were incomplete.

Tools created by the GNU Project include the GNU C Compiler (GCC), the GNU C Library (glibc), and the GNU Debugger (GDB).

>#### **Fun Fact**
>GNU is a recursive acronym which stands for **G**nu's **n**ot **U**NIX.

## Linux
With all of this stuff with UNIX and GNU going on, in 1990 a student named Linus Torvalds was required to read the book *Operating Systems: Design and Implementation* by Andrew S. Tannenbaum, which included a copy of an operating system called MINIX which the author had created and made available only for educational use. He became curious about operating systems, and began working on a free and open kernel. A coworker who was in charge of their FTP server named the project *Linux* (a mixture of Linus and the x suffix used in many UNIX based operating systems) on the server. Combined with many of the already UNIX compatible GNU utilities and tools, Linux became really popular because it worked well, was free, and helped get away from the OS monopoly held by Microsoft in the 90s.

## Modern Linux
Today, when you install Linux, you have a choice between many different **distributions**. A distribution is a combination of several components. Normally, they use the Linux kernel, tools from GNU, a desktop environment (a graphical user interface instead of just a command line), and other software packages that add functionallity.

Today, most distributions fall into one of a few families: BSD based, Red Hat based, or Debian based. A few common ones are listed.

### BSD Based
BSD based OSs are not strictly Linux because they don't use the Linux kernel, but they do operate similarly. In 1975, Ken Thopmson took a sabbatical from Bell Labs and taught at Berkeley as a visiting professor. They had been early adopters of UNIX and had built a lot of tools to imporve it, calling their version Berkeley Unix. BSD stands for **B**erkeley **S**oftware **D**istribution. Some common descendants include:

FreeBSD:
