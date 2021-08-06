DEBUG = 0
OBJ = \
	charset.o jymain.o luafun.o mainmap.o piccache.o sdlfun.o

HEADERS = \
	config.h list.h luafun.h
OD_TOOLCHAIN ?= /opt/aarch64-buildroot-linux-gnu_sdk-buildroot/
CC = $(OD_TOOLCHAIN)bin/aarch64-buildroot-linux-gnu-gcc
CXX = $(OD_TOOLCHAIN)bin/aarch64-buildroot-linux-gnu-g++
TARGET = jysdllua

BASEFLAGS = -g3 -D_DEBUG=0
#BASEFLAGS = -s -O3
SYSROOT     := $(shell $(CC) --print-sysroot)
SDL_CFLAGS  := $(shell $(SYSROOT)/usr/bin/sdl-config --cflags)
SDL_LIBS    := $(shell $(SYSROOT)/usr/bin/sdl-config --libs)

CFLAGS = ${BASEFLAGS} $(SDL_CFLAGS)
ifeq ($(DEBUG),1)
  CFLAGS += -I/usr/include/lua5.1/
endif
LDFLAGS = ${BASEFLAGS} $(SDL_LIBS) -lSDL_image -lSDL_mixer -lSDL_ttf -llua

#CFLAGS += -DHAS_SDL_MPEG=1
#LDFLAGS += -lsmpeg

all: ${TARGET}

${TARGET}: ${OBJ}
	${CXX} ${LDFLAGS} -o ${TARGET} ${OBJ}

clean:
	rm -f *.o ${TARGET}

distclean:
	rm -f *.o ${TARGET}

%.o:    %.cpp ${HEADERS}
	${CXX} ${CFLAGS} -c $< -o $@

%.o:    %.c ${HEADERS}
	${CC} ${CFLAGS} -c $< -o $@

