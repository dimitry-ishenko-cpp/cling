# Cling - The Interactive C++ Interpreter

This repository is a clone of the [Cling](https://root.cern/cling/) interactive
C++ interpreter from CERN. It includes several patches that do the following:

* Allow it to be built against patched external
[LLVM/Clang](https://github.com/dimitry-ishenko-cpp/llvm-toolchain-9); and
* Enable easy Debian packaging.

Both Cling and [xeus-cling](https://github.com/dimitry-ishenko-cpp/xeus-cling)
(a C++ Jupyter kernel built on top of Cling), along with other supporting
packages can be conveniently installed using
[ppa:ppa-verse/cling](https://launchpad.net/~ppa-verse/+archive/ubuntu/cling).

Building instructions:

```bash
p=cling b=debian # or focal or impish

# clone this repo
git clone -b ${b} --depth 1 https://github.com/dimitry-ishenko-cpp/${p}.git
r=$(cd ${p} && git log -n1 --oneline --no-decorate `git describe --tags --abbrev=0` | cut -d/ -f2)
v=${r%-*}
v=${v#*:}

# build source package
dpkg-source -b ${p}

# build .deb package locally...
sudo pbuilder build ${p}_${r}.dsc

# ...or generate .changes file and upload it to a PPA
# NB: change -sa to -sd when upgrading
(cd ${p} && dpkg-genchanges -S -sa -O../${p}_${r}_amd64.changes)

debsign ${p}_${r}_amd64.changes
dput ppa:... ${p}_${r}_amd64.changes

# share and enjoy
```
