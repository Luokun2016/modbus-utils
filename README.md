modbus-utils
============

Modbus client and server command line tools based on libmodbus.

NOTE:
Both apps are linked with libmodbus library. After repository is pulled do the following:

compilation
===========

## option 1 (cmake)

```sh
$ git clone https://github.com/Krzysztow/modbus-utils
$ cd modbus-utils
$ git submodule update --init
$ mkdir build
$ cd build
$ cmake ..
$ make 
```

## option 2

#assumes you are in a root of the repository

#go to libmodbus dir and compile it

cd ./libmodbus
./configure
./make

#as a result *.so libraries are in export ./src/.libs/ directory

#get back to the root

cd ..
gcc ./modbus_client/modbus_client.c -I./common -I./libmodbus/src/ -L./libmodbus/src/.libs/ -lmodbus -o mbClient
gcc ./modbus_server/modbus_server.c -I./common -I./libmodbus/src/ -L./libmodbus/src/.libs/ -lmodbus -o mbServer

running
=======


# 静态编译modbuslib
```
cd libmodbus

参考 MEADME

./configure --enable-static
make
make insatll
```

# 设置动态搜索路径为当前运行目录
```
gcc ./modbus_client/modbus_client.c -I./common -I./libmodbus/src/ -L./libmodbus/src/.libs/ -lmodbus -Wl,-rpath,. -o mbClient

gcc ./modbus_server/modbus_server.c -I./common -I./libmodbus/src/ -L./libmodbus/src/.libs/ -lmodbus -Wl,-rpath,. -o mbServer

将libmodbus.so.5放入程序执行目录
```

# 编译静态链接库
```
gcc ./modbus_client/modbus_client.c -I ./common -I ./libmodbus/src -l:libmodbus.a -o modbus_client
gcc ./modbus_server/modbus_server.c -I ./common -I ./libmodbus/src -l:libmodbus.a -o modbus_server
```

If modbus libraries are not in a default location (either it's needed to move libraries to app location or set
appropriate environment variable):
- on linux it would be:
  1) LD_LIBRARY_PATH=./libmodbus/src/.libs/ ./mbClient OR
  2) export LD_LIBRARY_PATH=./libmodbus/src/.libs/ and then run ./mbClient

usage
=====

Run apps with no arguments, descriptive help information will be provided.
