#
# This is the Makefile for the readline examples subdirectory.
#
# Copyright (C) 1994 Free Software Foundation, Inc.

# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2, or (at your option)
# any later version.

# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.

# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA 02111 USA.
RL_LIBRARY_VERSION = 5.2

SHELL = /bin/sh
RM = rm -f

srcdir = /usr/share/doc/libreadline5/examples
VPATH = .:/usr/share/doc/libreadline5/examples
top_srcdir = /usr/include/readline/
BUILD_DIR = .

# Support an alternate destination root directory for package building
DESTDIR =

DEFS = -DHAVE_CONFIG_H
CC = ccache icc
CFLAGS = -g -O2 -fdebug-prefix-map=/dev/shm/systemd/test/deps/test/lvm2/readline5/readline5-5.2+dfsg=. -Wformat -march=native -pipe -fstack-security-check -Wformat-security -g -O2
LOCAL_CFLAGS =  -DREADLINE_LIBRARY -DRL_LIBRARY_VERSION='"$(RL_LIBRARY_VERSION)"'
CPPFLAGS = -Wdate-time -D_FORTIFY_SOURCE=2

INCLUDES = -I$(srcdir) -I$(top_srcdir) -I..

CCFLAGS  = $(DEFS) $(LOCAL_CFLAGS) $(CPPFLAGS) $(INCLUDES) $(CFLAGS)
LDFLAGS = -g -L.. -Wl,-z,relro -Wl,--as-needed,--gc-sections,--relax

PURIFY = 

READLINE_LIB = ../libreadline.a
HISTORY_LIB = ../libhistory.a

TERMCAP_LIB = -lcurses

.c.o:
	${RM} $@
	$(CC) $(CCFLAGS) -c $<

EXECUTABLES = fileman rltest rl rlcat rlversion histexamp 
OBJECTS = fileman.o rltest.o rl.o rlcat.o rlversion.o histexamp.o

all: $(EXECUTABLES)
everything: all

rl: rl.o $(READLINE_LIB)
	$(PURIFY) $(CC) $(LDFLAGS) -o $@ rl.o $(READLINE_LIB) $(TERMCAP_LIB)

rlcat: rlcat.o $(READLINE_LIB)
	$(PURIFY) $(CC) $(LDFLAGS) -o $@ rlcat.o $(READLINE_LIB) $(TERMCAP_LIB)

fileman: fileman.o $(READLINE_LIB)
	$(PURIFY) $(CC) $(LDFLAGS) -o $@ fileman.o $(READLINE_LIB) $(TERMCAP_LIB)

rltest: rltest.o $(READLINE_LIB)
	$(PURIFY) $(CC) $(LDFLAGS) -o $@ rltest.o $(READLINE_LIB) $(TERMCAP_LIB)

rlptytest: rlptytest.o $(READLINE_LIB)
	$(PURIFY) $(CC) $(LDFLAGS) -o $@ rlptytest.o $(READLINE_LIB) $(TERMCAP_LIB)

rlversion: rlversion.o $(READLINE_LIB)
	$(CC) $(LDFLAGS) -o $@ rlversion.o $(READLINE_LIB) $(TERMCAP_LIB)

histexamp: histexamp.o $(HISTORY_LIB)
	$(PURIFY) $(CC) $(LDFLAGS) -o $@ histexamp.o -lhistory $(TERMCAP_LIB)

clean mostlyclean:
	$(RM) $(OBJECTS)
	$(RM) $(EXECUTABLES) *.exe

distclean maintainer-clean: clean
	$(RM) Makefile

fileman.o: fileman.c
rltest.o: rltest.c
rl.o: rl.c
rlversion.o: rlversion.c
histexamp.o: histexamp.c
rlcat.o: rlcat.c
rlptytest.o: rlptytest.c

fileman.o: $(top_srcdir)/readline.h
rltest.o: $(top_srcdir)/readline.h
rl.o: $(top_srcdir)/readline.h
rlversion.o: $(top_srcdir)/readline.h
histexamp.o: $(top_srcdir)/history.h
rlcat.o: $(top_srcdir)/readline.h $(top_srcdir)/history.h
rlptytest.o: $(top_srcdir)/readline.h $(top_srcdir)/history.h
