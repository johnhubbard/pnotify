pnotify
=======

Pnotify is patch to the Linux kernel. It lives next to inotify and fanotify, and borrows heavily from inotify in particular. The "p" stands for "process": pnotify monitors a process tree, rather than an inode.

Purpose
=======

The Linux kernel has inotify and fanotify, which provide notification of events within a filesystem. LWN has a nice article series (two articles so far) on it, here: http://lwn.net/Articles/605313/ . That write-up, especially in some of the comments, mentions that there are some missing pieces, that a user might want; specifically:

1) There is no effective way to monitor a directory tree, because if subdirectories are being created, the monitoring code will not get a chance to start monitoring those subdirectories, and so sub-subdirectory creation can happen, unnoticed.

2) There is no concept of "monitor all of the file accesses that are made by a process--including every child process of that process". Such a concept is of great value to systems (build systems, in particular) that would like to monitor file dependencies.

Therefore, this pnotify patch is meant to provide that missing piece. Pnotify looks a lot like inotify, but operates on processes, rather than on inodes.

There are two sub-projects, each of which is a complete fork of a Linux kernel tree:

pnotify-stable: early versions of internal patches, against selected linux-stable tree releases

pnotify-next: ongoing development, intended to be submitted upstream to kernel.org/LKML.
