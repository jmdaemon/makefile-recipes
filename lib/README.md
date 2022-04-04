# README

This Makefile is intended for small standalone libraries that only build the single library as a standalone target.

# Usage

1. Set your library's sources in `$(SRCS)`
2. Set your target library name in `$(TARGET_LIB)`, i.e (`libtarget.so`).
3. Run `make all`
