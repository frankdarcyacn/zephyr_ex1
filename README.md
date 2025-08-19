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
