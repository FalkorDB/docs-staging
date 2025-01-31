# Building dockers

The dockerfile examples in this directory are generated by the FalkorDB build system.  The build uses a [python script](https://github.com/RedisLabsModules/readies/blob/master/bin/dockerwrapper), to generate a dockerfile, on a per-platform basis, and build dockers from that. The dockerfile, calls various scripts from the [readies](https://github.com/redislabsmodules/readies) in order to further abstract everything away.  

## Requirements

In order to generate the dockerfile, or run the build system you need the following installed:

1. python > 3.6
1. [jinja](https://jinja.palletsprojects.com)   (pip install jinja2)
1. docker

## Manual Installation

As the docker build calls various scripts from within [readies](https://github.com/redislabsmodules/readies), the following are the series of commands triggered on a per-platform order. Note: these commands are literally what is run, meaning there is duplication.  The command list is generated by running **./sbin/system-setup.py -n** in the corresponding docker for each platform.  In the case of any script run from the *readies* repository, the associated script is similarly run with the **-n** option, producing the list below.

If manually installing packages, please ensure all commands are run via sudo, or through similar privilege escalation, ensuring that package installation will succeed.

### Centos 7

In addition to the above-mentioned requirements, it is assumed that epel repositories have been enabled.

```
yum install -q -y ca-certificates
yum install -q -y curl wget unzip
/usr/bin/python3 -m pip install --disable-pip-version-check wheel virtualenv
/usr/bin/python3 -m pip install --disable-pip-version-check setuptools --upgrade
/build/deps/readies/bin/enable-utf8
yum install -q -y git automake libtool autoconf
yum install -q -y redhat-lsb-core
yum groupinstall -y 'Development Tools'
yum install -q -y centos-release-scl
yum install -q -y devtoolset-10
yum install -q -y devtoolset-10-libatomic-devel
rm -f /etc/profile.d/scl-devtoolset-*.sh
yum install -q -y m4 libgomp
cd /tmp; build_dir=$(mktemp -d); cd $build_dir; wget -q -O peg.tar.gz https://github.com/gpakosz/peg/archive/0.1.18.tar.gz; tar xzf peg.tar.gz; cd peg-0.1.18; make; make install MANDIR=.; cd /tmp; rm -rf $build_dir
yum install -q -y valgrind
yum install -q -y astyle
yum install -q -y ca-certificates
yum install -q -y curl wget unzip
wget -q -O /tmp/cmake.sh https://github.com/Kitware/CMake/releases/download/v3.21.1/cmake-3.21.1-`uname`-`uname -m`.sh; sh /tmp/cmake.sh --skip-license --prefix=/usr/local; rm -f /tmp/cmake.sh
/usr/bin/python3 -m pip install --disable-pip-version-check psutil
/build/deps/readies/bin/getgcc
yum install -q -y python3-devel
/usr/bin/python3 -m pip install --disable-pip-version-check psutil
yum install -q -y git
/usr/bin/python3 -m pip install --disable-pip-version-check --no-cache-dir --ignore-installed git+https://github.com/redisfab/redis-py.git@3.5
/usr/bin/python3 -m pip install --disable-pip-version-check --no-cache-dir --ignore-installed redis-py-cluster
/usr/bin/python3 -m pip install --disable-pip-version-check --no-cache-dir --ignore-installed git+https://github.com/RedisLabsModules/RLTest.git@master
/usr/bin/python3 -m pip install --disable-pip-version-check --no-cache-dir --ignore-installed git+https://github.com/RedisLabs/RAMP@master
/usr/bin/python3 -m pip install --disable-pip-version-check -r tests/requirements.txt
```

### Ubuntu Bionic (18.04)

```
apt-get -qq update -y
apt-get -qq install -y ca-certificates
apt-get -qq install -y curl wget unzip
/usr/bin/python3 -m pip install --disable-pip-version-check wheel virtualenv
/usr/bin/python3 -m pip install --disable-pip-version-check setuptools --upgrade
/build/deps/readies/bin/enable-utf8
apt-get -qq install -y git automake libtool autoconf
apt-get -qq install -y locales
apt-get -qq update -y
apt-get -qq install -y build-essential
apt-get -qq install -y peg
apt-get -qq install -y valgrind
apt-get -qq install -y astyle
apt-get -qq update -y
apt-get -qq install -y ca-certificates
apt-get -qq install -y curl wget unzip
wget -q -O /tmp/cmake.sh https://github.com/Kitware/CMake/releases/download/v3.21.1/cmake-3.21.1-`uname`-`uname -m`.sh; sh /tmp/cmake.sh --skip-license --prefix=/usr/local; rm -f /tmp/cmake.sh
/usr/bin/python3 -m pip install --disable-pip-version-check psutil
apt-get remove -y python3-psutil
apt-get -qq update -y
apt-get -qq install -y build-essential
apt-get -qq install -y python3-dev
/usr/bin/python3 -m pip install --disable-pip-version-check psutil
apt-get -qq install -y git
/usr/bin/python3 -m pip install --disable-pip-version-check --no-cache-dir --ignore-installed git+https://github.com/redisfab/redis-py.git@3.5
/usr/bin/python3 -m pip install --disable-pip-version-check --no-cache-dir --ignore-installed redis-py-cluster
/usr/bin/python3 -m pip install --disable-pip-version-check --no-cache-dir --ignore-installed git+https://github.com/RedisLabsModules/RLTest.git@master
/usr/bin/python3 -m pip install --disable-pip-version-check --no-cache-dir --ignore-installed git+https://github.com/RedisLabs/RAMP@master
/usr/bin/python3 -m pip install --disable-pip-version-check -r tests/requirements.txt
```

### Debian Buster (10)

```
apt-get -qq update -y
apt-get -qq install -y ca-certificates
apt-get -qq install -y curl wget unzip
/usr/bin/python3 -m pip install --disable-pip-version-check wheel virtualenv
/usr/bin/python3 -m pip install --disable-pip-version-check setuptools --upgrade
/build/deps/readies/bin/enable-utf8
apt-get -qq install -y git automake libtool autoconf
apt-get -qq install -y locales
apt-get -qq update -y
apt-get -qq install -y build-essential
apt-get -qq install -y peg
apt-get -qq install -y valgrind
apt-get -qq install -y astyle
/build/deps/readies/bin/getcmake
apt-get -qq update -y
/usr/bin/python3 -m pip install --disable-pip-version-check psutil
apt-get remove -y python3-psutil
apt-get -qq update -y
apt-get -qq install -y build-essential
apt-get -qq install -y python3-dev
/usr/bin/python3 -m pip install --disable-pip-version-check psutil
apt-get -qq install -y git
/usr/bin/python3 -m pip install --disable-pip-version-check --no-cache-dir --ignore-installed git+https://github.com/redisfab/redis-py.git@3.5
/usr/bin/python3 -m pip install --disable-pip-version-check --no-cache-dir --ignore-installed redis-py-cluster
/usr/bin/python3 -m pip install --disable-pip-version-check --no-cache-dir --ignore-installed git+https://github.com/RedisLabsModules/RLTest.git@master
/usr/bin/python3 -m pip install --disable-pip-version-check --no-cache-dir --ignore-installed git+https://github.com/RedisLabs/RAMP@master
/usr/bin/python3 -m pip install --disable-pip-version-check -r tests/requirements.txt
```

### Alpine 3

```
apk add bash busybox python3
apk add -q ca-certificates
apk add -q curl wget unzip
/usr/bin/python3 -m pip install --disable-pip-version-check wheel virtualenv
/usr/bin/python3 -m pip install --disable-pip-version-check setuptools --upgrade
/build/deps/readies/bin/enable-utf8
apk add -q git automake libtool autoconf
apk add -q automake make autoconf libtool m4
apk add -q build-base musl-dev gcc g++
cd /tmp; build_dir=$(mktemp -d); cd $build_dir; wget -q -O peg.tar.gz https://github.com/gpakosz/peg/archive/0.1.18.tar.gz; tar xzf peg.tar.gz; cd peg-0.1.18; make; make install MANDIR=.; cd /tmp; rm -rf $build_dir
apk add -q valgrind
apk add -q astyle
apk add -q ca-certificates
apk add -q curl wget unzip
wget -q -O /tmp/cmake.sh https://github.com/Kitware/CMake/releases/download/v3.21.1/cmake-3.21.1-`uname`-`uname -m`.sh; sh /tmp/cmake.sh --skip-license --prefix=/usr/local; rm -f /tmp/cmake.sh
apk add -q linux-headers
apk add -q git
/usr/bin/python3 -m pip install --disable-pip-version-check --no-cache-dir --ignore-installed git+https://github.com/redisfab/redis-py.git@3.5
/usr/bin/python3 -m pip install --disable-pip-version-check --no-cache-dir --ignore-installed redis-py-cluster
/usr/bin/python3 -m pip install --disable-pip-version-check --no-cache-dir --ignore-installed git+https://github.com/RedisLabsModules/RLTest.git@master
/usr/bin/python3 -m pip install --disable-pip-version-check --no-cache-dir --ignore-installed git+https://github.com/RedisLabs/RAMP@master
/usr/bin/python3 -m pip install --disable-pip-version-check -r tests/requirements.txt
```