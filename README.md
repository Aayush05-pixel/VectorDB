# VectorDB
# VectorDB Local RAG Setup

## Overview

This project is a local Vector Database + RAG (Retrieval Augmented Generation) system using:

* C++
* httplib
* Ollama
* Gemma 3 / Local LLMs
* Web UI on localhost

---

## Prerequisites

### 1. Install Ollama

Download and install:

https://ollama.com

Verify:

```powershell
ollama list
```

Example output:

```text
gemma3:latest
```

---

### 2. Install MSYS2

Download:

https://www.msys2.org/

Install to:

```text
C:\msys64
```

---

### 3. Install GCC

Open **MSYS2 UCRT64**

Update:

```bash
pacman -Syu
```

Install compiler:

```bash
pacman -S mingw-w64-ucrt-x86_64-gcc
```

Verify:

```bash
g++ --version
```

Expected:

```text
g++ 16.x.x
```

---

## Clone Repository

```bash
git clone https://github.com/Aayush05-pixel/VectorDB.git
```

Open project:

```bash
cd VectorDB
```

---

## Project Files

```text
VectorDB/
│
├── main.cpp
├── httplib.h
├── index.html
├── README.md
└── .gitignore
```

---

## Compile

Open **MSYS2 UCRT64**

Navigate:

```bash
cd "/d/Users/Github Repo/VectorDB"
```

Compile:

```bash
g++ -std=c++17 -O2 main.cpp -o db.exe -lws2_32
```

Important:

```text
-O2
```

uses capital letter O, not zero.

---

## Run Server

```bash
./db.exe
```

Expected:

```text
=== VectorDB Engine ===
http://localhost:8080
20 demo vectors | 16 dims | HNSW+KD-Tree+BruteForce
```

---

## Open Web Interface

Open browser:

```text
http://localhost:8080
```

or

```text
http://127.0.0.1:8080
```

---

## Verify Server Running

Open PowerShell:

```powershell
netstat -ano | findstr 8080
```

Expected:

```text
LISTENING
```

---

## Verify Ollama

Check installed models:

```powershell
ollama list
```

Check Ollama API:

```powershell
curl http://localhost:11434/api/tags
```

Expected:

```json
{
  "models":[...]
}
```

---

## Run Gemma 3

```powershell
ollama run gemma3
```

Leave the terminal open.

---

## Common Errors

### Error

```text
g++: command not found
```

Solution:

Open **UCRT64** terminal instead of CLANG64.

Verify:

```bash
which g++
```

Expected:

```text
/ucrt64/bin/g++
```

---

### Error

```text
cannot find -lws_32
```

Wrong:

```bash
-lws_32
```

Correct:

```bash
-lws2_32
```

---

### Error

```text
Repository not found
```

Create repository first:

```text
VectorDB
```

Then:

```bash
git clone https://github.com/Aayush05-pixel/VectorDB.git
```

---

### Error

```text
undefined reference to WinMain@16
```

Make sure:

```cpp
int main() {
    return 0;
}
```

exists.

---

## Start Server Quickly

```bash
cd "/d/Users/Github Repo/VectorDB" && ./db.exe
```

---

## Auto Start Script

Create:

```text
start.sh
```

Contents:

```bash
#!/bin/bash
cd "/d/Users/Github Repo/VectorDB"
./db.exe
```

Make executable:

```bash
chmod +x start.sh
```

Run:

```bash
./start.sh
```

---

## Notes

* Keep db.exe running while using localhost.
* Keep Ollama running while using AI features.
* Retrieved context is shown in the UI.
* If answers ignore documents, improve the RAG prompt sent to Ollama.

---

Author: Aayush Savaliya
