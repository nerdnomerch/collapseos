# Collapse OS

*Bootstrap post-collapse technology*

Collapse OS is a Forth operating system and a collection of tools and
documentation with a single purpose: preserve the ability to program micro-
controllers through civilizational collapse.

It it designed to:

1. Run on minimal and improvised machines.
2. Interface through improvised means (serial, keyboard, display).
3. Edit text files.
4. Compile assembler source files for a wide range of MCUs and CPUs.
5. Read and write from a wide range of storage devices.
6. Assemble itself and deploy to another machine.

Additionally, the goal of this project is to be as self-contained as possible.
With a copy of this project, a capable and creative person should be able to
manage to build and install Collapse OS without external resources (i.e.
internet) on a machine of her design, built from scavenged parts with low-tech
tools.

# Getting started

Documentation is in text files in `doc/`. Begin with `intro.txt`.

Collapse OS can run on any POSIX platform and builds easily.
See `cvm/README` for instructions.

# Organisation of this repository

* blk.fs: Cross-arch Collapse OS filesystem's content. See below.
* cvm: A C implementation of Collapse OS, allowing it to run natively on any
       POSIX platform.
* doc: Documentation. Begin with intro.txt.
* arch: collection of makefiles that assemble Collapse OS on different machines.
        Also contains arch-specific blk.fs files. See below.
* tools: Tools for working with Collapse OS from "modern" environments. For
         example, tools for facilitating data upload to a Collapse OS machine
         through a serial port.
* emul: Tools for running Collapse OS in an emulated environment.

# blk.fs

There are multiple "blk.fs" files. One at the root of the Collapse OS package
and then one in each /arch subdirectory.

These are big text files which, collectively, contain the "real deal", that is,
the contents of Collapse OS' filesystem. That filesystem contains everything
that a post-collapse computer would manage, that is, all Forth and assembler
source code for the tools it needs to fulfill its goals.

The root blk.fs file is for cross-arch contents. blk.fs files in /arch/* are for
arch-specific contents. See doc/blk.txt for details.

The Collapse OS filesystem is a simple sequence of 1024 bytes blocks. That is
not very workable in the text editor of a modern system. `blk.fs` represents an
"unpacked" view of that block system. Each block (16 lines max per block, 64
chars max per line) begins with a marker indicating the block number of the
contents that follow.

Blocks must be in ascending order.

That file can be "packed" to a real blkfs with `/tools/blkpack`. A real blkfs
can be "unpacked" to its text file form with `/tools/blkunpack`.

# Emulation and dogfooding

Emulation used to be a central tool to developing new ports for Collapse OS.
On a POSIX platform, I would begin by creating an emulator for my target
machine, fool around, then when I thought I had something good, test on real
hardware for adjustments.

With the 6809 port, I wanted to take dogfooding more seriously and began
developing ports from Collapse OS itself on vintage machines. This allows me
to see opportunities for usability improvements and detect bugs much better than
when using a POSIX platform.

Because of that, the "emul" folder is no longer improved.
