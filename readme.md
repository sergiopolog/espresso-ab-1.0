## @sergiopolog: Fork with patches to allow compile it under Windows using MinGW.

Some POSIX resources and system calls which are not supported on Windows platform were removed (that probably don't update the behaviour of the app).
They are located in files:
* cpu_time.c
* signature.c
* util_signature.c

# Compiling:

Use MinGW under Windows to compile it. Some dependencies are needed to be previously installed:

```
pacman -S \
	autoconf-wrapper 15-1 \
	autoconf2.13 2.13-5 \
	autoconf2.69 2.69-2 \
	autoconf2.71 2.71-1 \
	automake-wrapper 11-4 \
	automake1.11 1.11.6-6 \
	automake1.12 1.12.6-6 \
	automake1.13 1.13.4-7 \
	automake1.14 1.14.1-6 \
	automake1.15 1.15.1-4 \
	automake1.16 1.16.5-1 \
	base 2020.12-1 \
	libtool 2.4.6-11 \
	make 4.3-1 \
	mingw-w64-x86_64-gcc 10.3.0-2 \
	mingw-w64-x86_64-libc++ 12.0.0-7 \
	mingw-w64-x86_64-lld 12.0.0-7
```

> Some packages might not be in the official repositories. Search and download files separately and install them using: 
> ```pacman -U autoconf-wrapper-15-1-any.pkg.tar.zst```


> You may need to use the following automake command if some error raises when compiling:
> ```automake --add-missing```

# TO-DO:

Rewrite removed code with windows native code.

# Original ReadMe follows:

This espresso source files have been patched so that it can be compiled with gcc 4.2.1 distributed with xcode 8 and gcc 5.4.0 on ubuntu 16.04. Below is the readme from the original author where I cloned these source files from. 

psksvp@gmail.com

~~~
This distribution is just a reworked version of the c. 1989 Berkeley
espresso source code.  All I've done is cut the number of files down
to just what is required for a modern POSIXy OS and made those files
more ISO-C compliant.  This should make building espresso a little
easier in these more standards compliant times.

See the file COPYING for the original code licence.  All kudos to the
original authors.

- Andrew
~~~

See below for an example input and output from espresso.

~~~
The pla for minterm List(0, 1, 3, 7, 8, 9, 11, 15) with 4 predicates (p0 ,p1, p2, p3) looks like below. .e indicates the end of input and output.

      -----------------------------
      .i 4
      .o 1
      0000 1
      0001 1
      0010 0
      0011 1
      0100 0
      0101 0
      0110 0
      0111 1
      1000 1
      1001 1
      1010 0
      1011 1
      1100 0
      1101 0
      1110 0
      1111 1
      .e
      ------------------------------

      The output is below, which indicates the simplify terms [[!p1, !p2], [p2, p3]] --> ((!p1 || !p2) && (p2 || p3)) from -00- and --11

      ------------------------------
      .i 4
      .o 1
      .p 2
      -00- 1
      --11 1
      .e
      ------------------------------
~~~
