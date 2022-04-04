# Makefile Recipes

This repository contains various Makefile recipes for C and/or C++ projects.

Feel free to use any of the Makefile recipes in these directories for your own projects.

## Usage

Drop one of these recipes into your projects, and follow the instructions to add your sources. Happy hacking!

## Including other Makefile projects

To include other people's libraries as a dependency use this snippet:

These instructions assume you have the sources in a top level folder called `subprojects`.

These instructions also assume you have already cloned the subproject into `subprojects`.

### Instructions

1. Include the dependency headers in `$(CFLAGS)` with `-Isubprojects/$(SUBPROJECT_NAME)`.
2. Link the dependency as a library in `$(LDFLAGS)` with `-Lsubprojects/$(SUBPROJECT_NAME)` and `-l$(DEP_NAME)`.
3. Ensure the library is built beforehand (by following the instructions to build the dependency) or include a rule to build the project with the library.

For the latter in step 3, you can use a snippet like:

``` Makefile

debug release: prep subprojects $(BUILD_EXEC)

# Build all the subprojects
subprojects: $(DEP_NAME)
	$(CC) $(CFLAGS) $(TARGET_FLAGS) -o $(DEP_NAME) $^

# Compile the executable binary target and its object files
$(BUILD_EXEC): $(BUILD_OBJS)
	$(CC) $(CFLAGS) $(TARGET_FLAGS) -o $(BUILD_EXEC) $^

# Compile all object targets in $(BUILD_DIR)
$(BUILD_DIR)/%.o: $(SRC_PREFIX)/%.c
	$(CC) -c $(CFLAGS) $(TARGET_FLAGS) -o $@ $<

```

## Building library and binary targets

To build a library and binary target for the same project, you can use the `lib-exec-dbg-rel` Makefile recipe.

Happy hacking!

## Support for multiple operating systems

To support multiple operating systems, you can include this snippet at the top of your Makefile:

``` Makefile
#
# Operating System Settings
#
ifeq ($(OSTYPE),cygwin)
	CLEANUP=rm -f
	MKDIR=mkdir -p
	TARGET_EXTENSION=out
else ifeq ($(OS),Windows_NT)
	CLEANUP=del /F /Q
	MKDIR=mkdir
	TARGET_EXTENSION=exe
else
	CLEANUP=rm -f
	MKDIR=mkdir -p
	TARGET_EXTENSION=out
endif
```

This will use `del` on Windows, and `rm -f` on Linux.
