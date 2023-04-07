# insani.org Modified configure and Makefile for onscripter-en
insani.org modified configure and Makefile for the onscripter-en build system, capable of building an x86-64 binary for onscripter-en on MSYS2 (MINGW64).  If you are interested in this, you are either Galladite27 or chaoskaiser72.

Unnatural things have been done to make this Makefile work on MSYS2.  Primarily, the existing build system for ONScripter-EN makes assumptions that fail -- for instance, it creates and compiles code to test for dependencies, but those code snippets *simply fail to compile* in MSYS2, causing cascade failures of dependency build.  I am well aware that this has not been done in the most elegant fashion, but I have found this level of disassembly necessary to begin to plumb the depths of *why* the onscripter-en build system fails as hard as it does on MSYS2.

Preliminary findings follow:

- The build system was written against the original MSYS, which is radically different from MSYS2 in a number of ways.
- Windows system includes and libraries that should work simply *are not properly included or linked* by this build system, causing "undefined reference to '__imp_uwu'" errors everywhere.
- extlibs build fails 100% of the time, in part due to the code snippet compilation issue noted above
- The build system makes faulty assumptions about 32/64-bit, which makes me think that there is a syntax error somewhere in the configure script that causes this behavior (it is present even when compiling for a 32-bit target)
- The build system actually assumes extlibs *even when you have system versions of the libraries in question*, which can lead to cascade failures during the link stage
- -Werror is a monumental mistake; you will simply be unable to compile on Windows if you leave it at that
  - Use -Wall instead
- **OYABB INSANITY SPIRIT IS ALIVE :3**
