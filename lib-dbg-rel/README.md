# README

This Makefile recipe will build a library in either debug or release configuration.
The recipe will generate the following structure:
    - build/debug/lib
    - build/release/lib

## Usage

1. Specify your library's sources in the `$(LIB_SRCS)` variable
2. Set your target library's name in `$(LIB)`.
3. Run `make lib`
