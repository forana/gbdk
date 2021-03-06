# Generated automatically from Makefile.in by configure.
#
#
#

VERSION         = 2.3.1
VERSIONHI       = 2
VERSIONLO       = 3
VERSIONP        = 1

SHELL		= /bin/sh
CPP		= gcc -E
INSTALL		= /usr/bin/install -c
CP              = cp

PRJDIR		= ../..
INCDIR		= $(PRJDIR)/device/include

CC		= $(PRJDIR)/bin/sdcc
CPP		= $(PRJDIR)/bin/sdcpp

prefix          = /opt/gbdk
exec_prefix     = ${prefix}
bindir          = ${exec_prefix}/bin
libdir          = ${exec_prefix}/lib
datadir         = ${prefix}/share
sdcc_datadir    = ${prefix}/share/sdcc
includedir      = ${prefix}/include
mandir          = ${prefix}/man
man1dir         = $(mandir)/man1
man2dir         = $(mandir)/man2
infodir         = ${prefix}/info
srcdir          = .

CPPFLAGS        = -I$(INCDIR)
CFLAGS		= $(MODELFLAGS) --nostdinc --nostdlib

BUILDDIR        = build
# Default
PORT            = z80
PORTDIR         = $(BUILDDIR)/$(PORT)

SOURCES		= _atoi.c _atol.c _autobaud.c _bp.c _schar2fs.c \
		  _decdptr.c _divsint.c _divslong.c _divuint.c \
		  _divulong.c _fs2schar.c _fs2sint.c _fs2slong.c \
		  _fs2uchar.c _fs2uint.c _fs2ulong.c _fsadd.c \
		  _fsdiv.c _fseq.c _fsgt.c _fslt.c _fsmul.c \
		  _fsneq.c _fssub.c _gptrget.c _gptrput.c \
		  _sint2fs.c _iscntrl.c _isdigit.c _isgraph.c \
		  _islower.c _isprint.c _ispunct.c _isspace.c \
		  _isupper.c _isxdigit.c _slong2fs.c _memcmp.c \
		  _memcpy.c _memset.c _modsint.c _modslong.c \
		  _moduint.c _modulong.c _mulint.c _mullong.c \
		  _ser.c _setjmp.c \
		  _spx.c _startup.c _strchr.c _strcmp.c _strcpy.c \
		  _strcspn.c _strlen.c _strncat.c _strncmp.c \
		  _strncpy.c _strpbrk.c _strrchr.c _strspn.c \
		  _strstr.c _strtok.c _uchar2fs.c _uint2fs.c \
		  _ulong2fs.c malloc.c serial.c ser_ir.c printfl.c \
		  printf_large.c vprintf.c puts.c gets.c \
		  assert.c _strcat.c time.c printf_fast.c

OBJECTS		= $(patsubst %.c,$(PORTDIR)/%.rel,$(SOURCES))

Z80SOURCES      = _atoi.c \
		  _iscntrl.c _isdigit.c _isgraph.c \
		  _islower.c _isprint.c _ispunct.c _isspace.c \
		  _isupper.c _isxdigit.c _memcmp.c \
		  _memcpy.c _memset.c \
		  _startup.c _strchr.c _strcmp.c _strcpy.c \
		  _strcspn.c _strlen.c _strncat.c _strncmp.c \
		  _strncpy.c _strpbrk.c _strrchr.c _strspn.c \
		  _strstr.c _strtok.c \
		  puts.c gets.c \
		  assert.c _strcat.c \
		  _modslong.c _modulong.c \
		  _mullong.c \
		  _divslong.c _divulong.c

Z80OBJECTS      = $(Z80SOURCES:%.c=$(PORTDIR)/%.o)

OEXT            = .rel

include incl.mk

# Compiling entire program or any subproject
# ------------------------------------------
all: checkconf models model-ds390 model-z80 model-gbz80

objects: build-dir $(OBJECTS) port-specific-objects lib-files

models:
	if [ "`grep mcs51 ../../ports.build`" = mcs51 ]; then \
	  for model in $(MODELS); do \
	    $(MAKE) MODELFLAGS="--model-$$model" PORT=$$model objects; \
	  done \
	fi

model-ds390:
	if [ "`grep ds390 ../../ports.build`" = ds390 ]; then \
	  $(MAKE) MODELFLAGS="-mds390" PORT=ds390 objects; \
	fi

model-z80:
	if [ "`grep z80 ../../ports.build`" = z80 ]; then \
	  $(MAKE) MODELFLAGS="-mz80" PORT=z80 objects-z80 OEXT=.o; \
	fi

model-gbz80:
	if [ "`grep z80 ../../ports.build`" = z80 ]; then \
	  $(MAKE) MODELFLAGS="-mgbz80" PORT=gbz80 objects-z80 OEXT=.o; \
	fi

objects-z80: build-dir $(Z80OBJECTS) port-specific-objects
	cd $(PORTDIR); ls *$(OEXT) > $(PORT).lib

build-dir: $(PORTDIR)

$(PORTDIR):
	mkdir -p $(PORTDIR)

port-specific-objects:
	if [ -d $(PORT) ]; then \
	  $(MAKE) -C $(PORT); \
	  cp -f $(PORT)/*.lib $(PORT)/*$(OEXT) $(PORTDIR); \
	fi

lib-files:
	cp *.lib $(PORTDIR)

# Compiling and installing everything and runing test
# ---------------------------------------------------
install: all installdirs
	cp -r $(BUILDDIR)/* $(sdcc_datadir)/lib
	cp -r ds390 gbz80 z80 *.c $(sdcc_datadir)/lib/src
	rm `find $(sdcc_datadir)/lib/src -name '*.rel' -or -name '*.dump*' -or -name '*.sym' -or -name '*.o' -or -name '*.lst' -or -name '*.asm'`

# Deleting all the installed files
# --------------------------------
uninstall:
	for hdr in ../include/*.h; do rm -f $(sdcc_datadir)/include/$$hdr; done
	for cfl in *.c; do rm -f $(sdcc_datadir)/lib/$$cfl; done
	for model in $(MODELS); do \
	  rm -rf $(sdcc_datadir)/lib/$$model; \
	done
	rm -rf $(sdcc_datadir)/lib/ds390


# Performing self-test
# --------------------
check:


# Performing installation test
# ----------------------------
installcheck:


# Creating installation directories
# ---------------------------------
installdirs:
	[ -d $(sdcc_datadir)/lib ] || mkdir -p $(sdcc_datadir)/lib
	for model in $(MODELS); do \
	 [ -d $(sdcc_datadir)/lib/$$model ] || \
	 mkdir -p $(sdcc_datadir)/lib/$$model; \
	done
	[ -d $(sdcc_datadir)/lib/ds390 ] || mkdir -p $(sdcc_datadir)/lib/ds390
	mkdir -p $(sdcc_datadir)/lib/src

# Creating dependencies
# ---------------------
dep: Makefile.dep

Makefile.dep: $(SOURCES) $(INCDIR)/*.h
	rm -f Makefile.dep
	for i in $(SOURCES); do \
	  $(CPP) -lang-c++ -M $(CPPFLAGS) $$i >$${i}.dep; \
	  cat $${i}.dep >>Makefile.dep; \
	  rm $${i}.dep; \
	done

include Makefile.dep
include clean.mk

# My rules
# --------

.SUFFIXES: .rel .o

$(PORTDIR)/%$(OEXT): %.c
	$(CC) $(CPPFLAGS) $(CFLAGS) -c $<
	mv -f `basename $@` $@
	mv -f `basename $@ $(OEXT)`.asm $(PORTDIR)

# Remaking configuration
# ----------------------
checkconf:
	@if [ -f $(PRJDIR)/devel ]; then\
	  $(MAKE) -f $(srcdir)/conf.mk srcdir="$(srcdir)" PRJDIR="$(PRJDIR)" \
	  freshconf;\
	fi

# End of main_in.mk/main.mk
