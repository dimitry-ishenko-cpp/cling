# Cling - The Interactive C++ Interpreter

This repository is a clone of the [Cling](https://root.cern/cling/) interactive
C++ interpreter from CERN. It includes several patches that do the following:

* Allow it to be built against patched external
[LLVM/Clang](https://github.com/dimitry-ishenko-cpp/llvm-toolchain); and
* Enable easy Debian packaging.

Both Cling and [xeus-cling](https://github.com/dimitry-ishenko-cpp/xeus-cling)
(a C++ Jupyter kernel built on top of Cling), along with other supporting
packages can also be conveniently installed through
[ppa:ppa-verse/cling](https://launchpad.net/~ppa-verse/+archive/ubuntu/cling).