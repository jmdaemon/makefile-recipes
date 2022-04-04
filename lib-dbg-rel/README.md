# README

This Makefile recipe will build a library in either debug or release configuration.
The recipe will generate the following structure:
    - build/debug/lib
    - build/release/lib

## Usage

To use this recipe just specify your library's sources in the `$(LIB_SRCS)` variable, and your target library's name in `$(LIB)`.
