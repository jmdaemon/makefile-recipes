#
# Compiler flags
#
CFLAGS = -Wall -Wextra -Iinclude
LDFLAGS = 

#
# Prefixes
#
# These are used to generate the build structure:
# build/{debug,release}/{lib}
BUILD_PREFIX = build
SRC_PREFIX = src
LIB_PREFIX = lib

#
# Library
#
# Builds the project as a library
CFLAGS_LIB = -fPIC -g
LDFLAGS_LIB = -shared
LIB_SRCS = $(SRCS)
LIB_OBJS = $(LIB_SRCS:.c=.o)
LIB = 

.PHONY: all clean prep debug release lib remake

# Default build
all: prep release

#
# Build settings
#

# Set install
ifeq ($(PREFIX),)
    PREFIX := /usr/local
endif

# Release build settings
TARGET:=release
TARGET_FLAGS:= -O3 -DNDEBUG $(LDFLAGS)

# Debug build settings
ifeq ($(filter debug,$(MAKECMDGOALS)),debug)
TARGET=debug
TARGET_FLAGS= -g -O0 -DDEBUG $(LDFLAGS)
endif

# Library build settings
# TARGET_FLAGS: 	The library flags to build the library
# BUILD_LIB: 			The directory of the target library
# BUILD_LIB_OBJS: The object files of the library target
ifeq ($(filter lib,$(MAKECMDGOALS)),lib)
TARGET_FLAGS = $(LDFLAGS) $(CFLAGS_LIB) $(LDFLAGS_LIB) 
BUILD_LIB = $(BUILD_DIR)/$(LIB_PREFIX)/$(LIB)
BUILD_LIB_OBJS = $(addprefix $(BUILD_DIR)/, $(LIB_OBJS))
endif

# Rules

## Install/Uninstall
install: release $(BUILD_LIB)
	install $(BUILD_LIB) $(DESTDIR)$(PREFIX)/bin/$(EXE)

uninstall: release $(BUILD_LIB)
	rm -f $(DESTDIR)$(PREFIX)/bin/$(EXE)

#
# Library builds
#
lib: prep-library $(BUILD_LIB)

# Compiles the shared library target and its object files
$(BUILD_LIB): $(BUILD_LIB_OBJS) 
	$(CC) $(CFLAGS) $(TARGET_FLAGS) -o $@ $^

#
# Debug/Release builds
#
debug release: prep-library $(BUILD_LIB)

# Compile all object targets in $(BUILD_DIR)
$(BUILD_DIR)/%.o: $(SRC_PREFIX)/%.c
	$(CC) -c $(CFLAGS) $(TARGET_FLAGS) -o $@ $<

#
# Other rules
#
# prep, prep-lirary: Creates the directories for the bin and lib targets

# Creates build/$(LIB_PREFIX)/lib
prep-library:
	@mkdir -p $(BUILD_DIR)/$(LIB_PREFIX)

remake: clean all

clean:
	rm -f $(RELEXE) $(RELOBJS) $(DBGEXE) $(DBGOBJS)
