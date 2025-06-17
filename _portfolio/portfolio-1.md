---
title: "FuzzCraft"
date: 2025-06-15
excerpt: "A high-performance web path fuzzer written in Go with intelligent filtering and progress tracking.<br/><img src='/images/fuzzcraft.png'>"
collection: portfolio
---


## Features

- 🚀 Multi-threaded fuzzing with adjustable concurrency
- 🎨 Color-coded output for different HTTP status codes
- 🔍 Status code filtering (single codes or ranges)
- 📊 Real-time progress reporting
- 💾 Results saving to file
- 🔒 Supports HTTPS with configurable certificate verification

## Installation

### From Source
```bash
git clone https://github.com/DivyanshGohil/FuzzCraft.git
cd FuzzCraft
go build
```
## Usage
```bash
./FuzzCraft -u http://example.com/FUZZ -w wordlists/common.txt [options]
```

### Basic Option
|**Flag**|**Description**                     |**Example**               |
|--------|------------------------------------|--------------------------|
|-u      |Target URL with FUZZ placeholder    |http://example.com/FUZZ   |
|-w      |Path to wordlist file               |wordlists/common.txt      |
|-t      |Number of Threads (default 50)      |-t 100                    |
|-fc     |Filter status codes (comma or range)|-fc 200,301 or -fc 200-399|

### Advanced Option
|**Flag**|**Description**                 |
|--------|--------------------------------|
|-X      |HTTP method (default: GET)      |
|-H      |Custom headers (comma separated)|
|-d      |POST/PUT data                   |
|-o      |Output file for results         |
|-k      |Allow insecure SSL connections  |

## Basic Examples
1. Basic Fuzzing
```bash
./FuzzCraft -u http://test.com/FUZZ -w wordlists/common.txt
```
2. Filter for successful responses
```bash
./FuzzCraft -u https://test.com/FUZZ -w big_wordlist.txt -fc 200-399 -k
```
3. Save results and use 100 threads
```bash
./FuzzCraft -u http://test.com/FUZZ -w wordlists/common.txt -o results.txt -t 100
```
