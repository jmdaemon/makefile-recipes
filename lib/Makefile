# Settings
CC = gcc
RM = rm -f

# Flags
CFLAGS = -fPIC -Wall -Wextra -O2 -g
LDFLAGS = -shared

# Target
TARGET_LIB = 

# Source & Object Files
SRCS = 
OBJS = $(SRCS:.c=.o)

# Rules

.PHONY: all clean

all: ${TARGET_LIB}

# Build the target library
$(TARGET_LIB): $(OBJS)
	$(CC) ${LDFLAGS} -o $@ $^

# Build the library dependencies
$(SRCS:.c=.d):%.d:%.c
	$(CC) $(CFLAGS) -MM $< >$@

include $(SRCS:.c=.d)

clean:
	-${RM} ${TARGET_LIB} ${OBJS} $(SRCS:.c=.d)
