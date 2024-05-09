# Zephyr Getting Started Guide on Windows for ST NUCLEO-L476RG

Installation instructions are valid for 09-05-2024
Installation procedure are based on [Getting Started Guide](https://docs.zephyrproject.org/latest/develop/getting_started/index.html)

## 1. Install Dependencies

Go to official sites and download
- [Cmake](https://cmake.org/download/) (3.29.3)
- [Python](https://www.python.org/ftp/python/3.12.3/python-3.12.3-amd64.exe) (3.12.3)
- [Ninja](https://ninja-build.org/) ```winget install Ninja-build.Ninja```
- [7-Zip](https://www.7-zip.org/) ```winget install 7z```
- [MSYS2](https://www.msys2.org/)
- Install **gperf** with **msys2** ```pacman -S msys/gperf```
- Install **dtc** with **msys2** ```pacman -S msys/dtc```
- Add ```C:\msys64\usr\bin``` to Environment variable so west can find **dtc** and **gperf** later 

## 2. Get Zephyr and install Python dependencies

Commands are supposed to be run in **cmd.exe**

1. Create a new virtual environment:

```python -m venv zephyrproject\.venv```

2. Activate the virtual environment:

```zephyrproject\.venv\Scripts\activate.bat```

3. Install **west**:

```pip install west```

4. Get the Zephyr source code:

```
west init zephyrproject
cd zephyrproject
west update
```

5. Export a Zephyr CMake package. This allows CMake to automatically load boilerplate code required for building Zephyr applications.
 
```west zephyr-export```

6. Zephyr’s scripts\requirements.txt file declares additional Python dependencies.

```pip install -r .\zephyrproject\zephyr\scripts\requirements.txt```

## 3. Download Zephyr SDK

Download [Full SDK bundle](https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.16.6/zephyr-sdk-0.16.6_windows-x86_64.7z) from https://github.com/zephyrproject-rtos/sdk-ng/releases/tag/v0.16.6

Extract it in %HOMEPATH% your User home directory - zephyr-sdk-0.16.6

```
cd zephyr-sdk-0.16.6
setup.cmd
```

## 4. Build Blinky

1. Go to ```zephyrproject\zephyr```

2. Run ```west boards``` to get the list of all supported boards. For me it's **nucleo_l476rg**

3. Build with 

```west build -p always -b nucleo_l476rg samples\basic\blinky```

## Flash the Sample

```west flash```

