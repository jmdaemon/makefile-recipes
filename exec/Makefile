CFLAGS = -Wall -Wextra
LDFLAGS = 

SRCS = $(wildcard *.c)
OBJS = $(SRCS:.c=.o)
EXE = 

.PHONY: clean build

build: $(OBJS)
    $(CC)  $(LDFLAGS) -o $@ $^

clean:
	rm -f $(OBJS) $(EXE)
