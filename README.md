# commonlib in ubuntu2204
## envirement
```
➜ uname -a
Linux undertable 5.15.0-118-generic #128-Ubuntu SMP Fri Jul 5 09:28:59 UTC 2024 x86_64 x86_64 x86_64 GNU/Linux


➜ gcc -v
Using built-in specs.
COLLECT_GCC=gcc
COLLECT_LTO_WRAPPER=/usr/lib/gcc/x86_64-linux-gnu/11/lto-wrapper
OFFLOAD_TARGET_NAMES=nvptx-none:amdgcn-amdhsa
OFFLOAD_TARGET_DEFAULT=1
Target: x86_64-linux-gnu
Configured with: ../src/configure -v --with-pkgversion='Ubuntu 11.4.0-1ubuntu1~22.04' --with-bugurl=file:///usr/share/doc/gcc-11/README.Bugs --enable-languages=c,ada,c++,go,brig,d,fortran,objc,obj-c++,m2 --prefix=/usr --with-gcc-major-version-only --program-suffix=-11 --program-prefix=x86_64-linux-gnu- --enable-shared --enable-linker-build-id --libexecdir=/usr/lib --without-included-gettext --enable-threads=posix --libdir=/usr/lib --enable-nls --enable-bootstrap --enable-clocale=gnu --enable-libstdcxx-debug --enable-libstdcxx-time=yes --with-default-libstdcxx-abi=new --enable-gnu-unique-object --disable-vtable-verify --enable-plugin --enable-default-pie --with-system-zlib --enable-libphobos-checking=release --with-target-system-zlib=auto --enable-objc-gc=auto --enable-multiarch --disable-werror --enable-cet --with-arch-32=i686 --with-abi=m64 --with-multilib-list=m32,m64,mx32 --enable-multilib --with-tune=generic --enable-offload-targets=nvptx-none=/build/gcc-11-XeT9lY/gcc-11-11.4.0/debian/tmp-nvptx/usr,amdgcn-amdhsa=/build/gcc-11-XeT9lY/gcc-11-11.4.0/debian/tmp-gcn/usr --without-cuda-driver --enable-checking=release --build=x86_64-linux-gnu --host=x86_64-linux-gnu --target=x86_64-linux-gnu --with-build-config=bootstrap-lto-lean --enable-link-serialization=2
Thread model: posix
Supported LTO compression algorithms: zlib zstd
gcc version 11.4.0 (Ubuntu 11.4.0-1ubuntu1~22.04)
```

## cmdline
copy from https://github.com/tanakh/cmdline.git

### build
header only

### usage
```
// include cmdline.h
#include "cmdline.h"

int main(int argc, char *argv[])
{
  // create a parser
  cmdline::parser a;

  // add specified type of variable.
  // 1st argument is long name
  // 2nd argument is short name (no short name if '\0' specified)
  // 3rd argument is description
  // 4th argument is mandatory (optional. default is false)
  // 5th argument is default value  (optional. it used when mandatory is false)
  a.add<string>("host", 'h', "host name", true, "");

  // 6th argument is extra constraint.
  // Here, port number must be 1 to 65535 by cmdline::range().
  a.add<int>("port", 'p', "port number", false, 80, cmdline::range(1, 65535));

  // cmdline::oneof() can restrict options.
  a.add<string>("type", 't', "protocol type", false, "http", cmdline::oneof<string>("http", "https", "ssh", "ftp"));

  // Boolean flags also can be defined.
  // Call add method without a type parameter.
  a.add("gzip", '\0', "gzip when transfer");

  // Run parser.
  // It returns only if command line arguments are valid.
  // If arguments are invalid, a parser output error msgs then exit program.
  // If help flag ('--help' or '-?') is specified, a parser output usage message then exit program.
  a.parse_check(argc, argv);

  // use flag values
  cout << a.get<string>("type") << "://"
       << a.get<string>("host") << ":"
       << a.get<int>("port") << endl;

  // boolean flags are referred by calling exist() method.
  if (a.exist("gzip")) cout << "gzip" << endl;
}
```
## spdlog
copy from https://github.com/gabime/spdlog.git

### build
header only

### usage

## concurrentqueue
copy from https://github.com/cameron314/concurrentqueue.git

### build
header only

### usage

## protobuf
copy from https://github.com/protocolbuffers/protobuf.git

### build
```
mkdir buildinstall
sudo apt-get install -y autoconf automake libtool
git checkout v3.6.1
git submodule update --init --recursive
./autogen.sh
./configure --prefix=/home/peter/sourcecode/protobuf/buildinstall
make -j8
make install
```
### usage

## yaml-cpp
### build
```
mkdir build
mkdir buildinstall
cd build
cmake -DYAML_BUILD_SHARED_LIBS=ON -DCMAKE_INSTALL_PREFIX=~/sourcecode/yaml-cpp/buildinstall ..
make
make install
```
### usage

## zeromq
### build
```
mkdir build
mkdir buildinstall
cd build
cmake .. -DCMAKE_INSTALL_PREFIX=~/sourcecode/libzmq/buildinstall
make 
make install
```
### usage
