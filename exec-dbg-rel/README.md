# README

This Makefile has the following features:
- Support debug builds with custom flags
- Support release builds with custom flags
- Create builds with the following structure:
    - build/debug/bin
    - build/release/bin
- Include headers in top level include directory
- Install binaries to /usr/local

## Usage

Specify your binary sources in the `$(SRCS)` variable,
and set your binary executable name in `$(EXE)`.
