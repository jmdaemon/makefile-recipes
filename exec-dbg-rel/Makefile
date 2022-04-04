#
# Compiler flags
#
CFLAGS = -Wall -Wextra -Iinclude
LDFLAGS = 

#
# Prefixes
#
# These are used to generate the build structure:
# build/{debug,release}/bin
BUILD_PREFIX = build
SRC_PREFIX = src
BIN_PREFIX = bin

#
# Project files
#
# Build the project as an executable binary
#
# Note: $(SRCS:.c=.o) replaces all *.c sources with *.o extensions
SRCS = 
OBJS = $(SRCS:.c=.o)
EXE  = 

.PHONY: all clean prep debug release remake

# Default build
all: prep release

# Set install
ifeq ($(PREFIX),)
    PREFIX := /usr/local
endif

#
# Build settings
#

# Release build settings
TARGET:=release
TARGET_FLAGS:= -O3 -DNDEBUG $(LDFLAGS)

# Debug build settings
ifeq ($(filter debug,$(MAKECMDGOALS)),debug)
TARGET = debug
TARGET_FLAGS = -g -O0 -DDEBUG $(LDFLAGS)
endif

# Executable settings
# BUILD_DIR: 	The directory of the target.
# BUILD_EXEC: The output directory of the binary target
# BUILD_OBJS: The object files of the binary target

BUILD_DIR = $(BUILD_PREFIX)/$(TARGET)
BUILD_EXEC= $(BUILD_DIR)/$(BIN_PREFIX)/$(EXE)
BUILD_OBJS= $(addprefix $(BUILD_DIR)/, $(OBJS))

# Rules

## Install/Uninstall
install: release $(BUILD_EXEC)
	install $(BUILD_EXEC) $(DESTDIR)$(PREFIX)/bin/$(EXE)

uninstall: release $(BUILD_EXEC)
	rm -f $(DESTDIR)$(PREFIX)/bin/$(EXE)

#
# Debug/Release builds
#
debug release: prep $(BUILD_EXEC)

# Compile the executable binary target and its object files
$(BUILD_EXEC): $(BUILD_OBJS)
	$(CC) $(CFLAGS) $(TARGET_FLAGS) -o $(BUILD_EXEC) $^

# Compile all object targets in $(BUILD_DIR)
$(BUILD_DIR)/%.o: $(SRC_PREFIX)/%.c
	$(CC) -c $(CFLAGS) $(TARGET_FLAGS) -o $@ $<

#
# Other rules
#

# prep: Creates the directories for the bin target

# Creates build/$(BIN_PREFIX)
prep:
	@mkdir -p $(BUILD_DIR)/$(BIN_PREFIX)

remake: clean all

clean:
	rm -f $(RELEXE) $(RELOBJS) $(DBGEXE) $(DBGOBJS)
