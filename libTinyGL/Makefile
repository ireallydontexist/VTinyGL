TARGET_LIB = libTinyGL.a
OBJS       = source/api.o source/list.o source/vertex.o source/init.o \
						 source/matrix.o source/texture.o source/misc.o source/clear.o \
						 source/light.o source/clip.o source/select.o source/get.o source/error.o \
						 source/zbuffer.o source/zline.o source/zdither.o source/ztriangle.o \
						 source/zmath.o source/image_util.o source/oscontext.o source/msghandling.o \
						 source/arrays.o source/specbuf.o source/memory.o source/vgl.o
INCLUDES   = include
SHADERS    = 

PREFIX  ?= ${VITASDK}/arm-vita-eabi
CC      = arm-vita-eabi-gcc
AR      = arm-vita-eabi-ar
CFLAGS  = -Wl,-q -Wall -O3 -I$(INCLUDES) -ffat-lto-objects -flto
ASFLAGS = $(CFLAGS)

all: $(TARGET_LIB)

debug: CFLAGS += -DDEBUG_BUILD
debug: all

$(TARGET_LIB): $(SHADERS) $(OBJS)
	$(AR) -rc $@ $^

clean:
	rm -rf $(TARGET_LIB) $(OBJS)

install: $(TARGET_LIB)
	@mkdir -p $(DESTDIR)$(PREFIX)/lib/
	cp $(TARGET_LIB) $(DESTDIR)$(PREFIX)/lib/
	@mkdir -p $(DESTDIR)$(PREFIX)/include/GL
	cp include/GL/gl.h $(DESTDIR)$(PREFIX)/include/GL
	cp include/GL/vgl.h $(DESTDIR)$(PREFIX)/include/GL
