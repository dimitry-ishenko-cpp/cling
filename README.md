# Cling - The Interactive C++ Interpreter

This repository is a clone of the [Cling](https://root.cern/cling/) interactive
C++ interpreter from CERN. It includes several patches that do the following:

* Allow it to be built against patched external
[LLVM/Clang](https://github.com/dimitry-ishenko-cpp/llvm-toolchain-9); and
* Enable easy Debian packaging.

Building instructions:

```bash
p=cling b=debian # or focal or impish

# clone this repo
git clone -b ${b} --depth 1 https://github.com/dimitry-ishenko-cpp/${p}.git
r=$(cd ${p} && git log -n1 --oneline --no-decorate `git describe --tags --abbrev=0` | cut -d/ -f2)
v=${r%-*}
v=${v#*:}

# create upstream tarball
cd ${p}
dh_make --createorig -p ${p}_${v}
cd ..

# build source package
dpkg-source -b ${p}

# build binary package locally...
sudo pbuilder build ${p}_${r}.dsc

# ...or generate .changes file and...
cd ${p}
dpkg-genchanges -S -sa -O../${p}_${r}_amd64.changes # -sa => -sd when upgrading
cd ..

# build in a PPA
debsign ${p}_${r}_amd64.changes
dput ppa:... ${p}_${r}_amd64.changes

# share and enjoy
```

Both Cling and [xeus-cling](https://github.com/dimitry-ishenko-cpp/xeus-cling)
(a C++ Jupyter kernel built on top of Cling), along with other supporting
packages can also be conveniently installed through
[ppa:ppa-verse/cling](https://launchpad.net/~ppa-verse/+archive/ubuntu/cling).