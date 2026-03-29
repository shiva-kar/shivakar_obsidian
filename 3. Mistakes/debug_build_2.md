# Debug build
debug: CFLAGS += -DDEBUG -O0 -fsanitize=address
debug: all