DropWatch
=========

[![Build Status](https://travis-ci.org/nhorman/dropwatch.svg?branch=master)](https://travis-ci.org/nhorman/dropwatch)

Thanks for Downloading Dropwatch!

What is Dropwatch?
------------------
Dropwatch is a project I started in an effort to improve the ability for
developers and system administrators to diagnose problems in the Linux Networking
stack, specifically in our ability to diagnose where packets are getting
dropped.  From my probing, I've come to the conclusion that there are four main
shortcomings in our current environment:

1) _Consolidation, or lack thereof._  Currently, if you would like to check on the
status of dropped packets in the kernel, you need to check at least 4 places,
and possibly more: The /proc/net/snmp file, the netstat utility, the tc utility,
and ethtool.  This project aims to consolidate several of those checks into one
tool, making it easier for a sysadmin or developer to detect lost packets

2) _Clarity of information._  Dropped packets are not obvious.  A sysadmin needs
to be intimately familiar with each of the above tools to understand which
events or statistics correlate to a dropped packet and which do not.  While that
is often self evident, it is also often not.  Dropwatch aims to improve that
clarity

3) _Ambiguity._  Even when a dropped packet is detected, the causes for those
dropped packets are not always clear.  Does a UDPInError mean the application
receive buffer was full, or does it mean its checksum was bad?  Dropwatch
attempts to disambiguate the causes for dropped packets.

4) _Performance._  Utilities can be written to aggregate the data in the various
other utilities to solve some of these problems, but such solutions require
periodic polling of several interfaces, which is far from optimal, especially
when lost packets are rare.  This solution improves on the performance aspect by
implementing a kernel feature which allows asynchronous notification of dropped
packets when they happen.

Building Dropwatch
------------------
Dropwatch uses the autotools suite (autoconf/automake) to build.  To build and install the utility run the following commands:
```
./autogen.sh
./configure
make
make install
```

Questions
---------
Feel free to email me directly at nhorman@tuxdriver.com with question, or if you
find a bug, open an issue here on the github page

Build Problems:
---------
Build within ubuntu18.04, it will ./configure with the message "configure: error: libreadline is required", solution:
sudo vim /usr/share/pkgconfig/readline.pc
```
Name: Readline
Description: Gnu Readline library for command line editing
URL: http://tiswww.cwru.edu/php/chet/readline/rltop.html
Version: 7.0
Requires.private: tinfo
Libs: -lreadline
Cflags: -I/usr/include/readline
```
and run ./configure again.


