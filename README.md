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
