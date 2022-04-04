# README

This Makefile supports
- All the features in exec-dbg-rel/Makefile
- All the features in lib/Makefile

You can build your project both as an executable and as a shared library
for other projects.

## Usage

## Binary target
1. Specify your binary sources in `$(SRCS)`
2. Specify your binary executable name in `$(EXE)`
3. Run `make debug` or `make release`

## Library target

1. Specify your library's sources in the `$(LIB_SRCS)` variable
2. Set your target library's name in `$(LIB)`.
3. Run `make lib`
