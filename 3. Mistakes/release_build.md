# Release build
release: CFLAGS += -DNDEBUG -O3
release: all