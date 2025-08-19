# zephyr_ex1

## Prerequisites

Set up the dependencies and tools needed to build Zephyr by following its
[Getting Started Guide](https://docs.zephyrproject.org/latest/develop/getting_started/index.html).

When this is complete, you should have a python environment in which [Zephyr's `west` tool](https://docs.zephyrproject.org/latest/develop/west/index.html) is available.

`west` is a multipurpose tool used extensively in development and test of applications using Zephyr, as outlined below.

## Workspace Setup

Create a top directory (eg. named `zephyr_workspace`) and clone this repo in it.

```
mkdir zephyr_workspace
cd zephyr_workspace
git clone <url for this repo> zephyr_ex1
```

Initialize the workspace (this just creates `.west/config`)...

```
zephyr_workspace> west init -l zephyr_ex1
```

Update the workspace - the following command pulls code from multiple git repos
and lays it out in the workspace as specified in `zephyr_ex1/west.yml`...

```
zephyr_workspace> west update
```

## Build and run on your host

To build the `hello_world` sample app to run on your host system...

```
zephyr_workspace> west build -b native_sim zephyr_ex1/samples/hello_world
```

Assuming this is successful, all generated build output should be
in the newly created `build` directory,
and you can directly run the `hello_world` executable as follow...
```
zephyr_workspace> build/zephyr/zephyr.exe
```

Alternatively you can build and run for the `qemu_x86` target as follows
(note that `-p` means "pristine" - any pre-existing `build` directory
is wiped before starting a new build)...

```
zephyr_workspace> west build -p -b qemu_x86 zephyr_ex1/samples/hello_world
zephyr_workspace> west build -t run
```

## Build for an ARM-based Nordic development board

Having the following Zephyr modules in `west.yml`...
```
          - cmsis_6
          - hal_nordic
```
means that their git repos should have been cloned under the directory `modules/hal`
when you ran `west update` and this means you should be able to
build for ARM-based Nordic development boards,
assuming other dependencies they may need are in place.

Let's use the [nRF5340 Development Kit](https://www.nordicsemi.com/Software-and-tools/Development-Kits/nRF5340-DK) as an example.

The Zephyr page for the
[nRF5340](https://docs.zephyrproject.org/latest/boards/nordic/nrf5340dk/doc/index.html)
contains information related to using Zephyr with this board.

To build `hello_world` for the nRF5340 SoC's application core (`cpuapp`)...
```
zephyr_workspace> west build -p -b nrf5340dk/nrf5340/cpuapp zephyr_ex1/samples/hello_world
```

[Programming and Debugging](https://docs.zephyrproject.org/latest/boards/nordic/nrf5340dk/doc/index.html#programming-and-debugging)
lists the "runners and associated west commands" supported based on different tools.

So, for example if you have the Segger JLink set up as instructed
you should be able to flash the images you built above by running...
```
zephyr_workspace> west flash -r jlink
```
and you should be able to start a GDB debugging session by running...
```
zephyr_workspace> west debug -r jlink
```
