#
# SSLeay/crypto/ts/Makefile
#

DIR=	ts
TOP=	../..
CC=	cc
INCLUDES= -I.. -I../../include
CFLAG = -g
INSTALL_PREFIX=
OPENSSLDIR=     /usr/local/ssl
INSTALLTOP=/usr/local/ssl
MAKEDEPPROG=	makedepend
MAKEDEPEND=	$(TOP)/util/domd $(TOP) -MD $(MAKEDEPPROG)
MAKEFILE=	Makefile
AR=		ar r

PEX_LIBS=
EX_LIBS=
 
CFLAGS= $(INCLUDES) $(CFLAG)

GENERAL= Makefile
TEST=
APPS=

LIB=$(TOP)/libcrypto.a
LIBSRC=	ts_err.c ts_req_utils.c ts_req_print.c ts_rsp_utils.c ts_rsp_print.c \
	ts_rsp_sign.c ts_rsp_verify.c ts_verify_ctx.c ts_lib.c ts_conf.c \
	ts_asn1.c
LIBOBJ= ts_err.o ts_req_utils.o ts_req_print.o ts_rsp_utils.o ts_rsp_print.o \
	ts_rsp_sign.o ts_rsp_verify.o ts_verify_ctx.o ts_lib.o ts_conf.o \
	ts_asn1.o

SRC= $(LIBSRC)

EXHEADER= ts.h
HEADER=	$(EXHEADER)

ALL=    $(GENERAL) $(SRC) $(HEADER)

top:
	(cd ../..; $(MAKE) DIRS=crypto SDIRS=$(DIR) sub_all)

test:

all:	lib

lib:	$(LIBOBJ)
	$(AR) $(LIB) $(LIBOBJ)
	$(RANLIB) $(LIB) || echo Never mind.
	@touch lib

files:
	$(PERL) $(TOP)/util/files.pl Makefile >> $(TOP)/MINFO

links:
	@$(PERL) $(TOP)/util/mklink.pl ../../include/openssl $(EXHEADER)
	@$(PERL) $(TOP)/util/mklink.pl ../../test $(TEST)
	@$(PERL) $(TOP)/util/mklink.pl ../../apps $(APPS)

install:
	@[ -n "$(INSTALLTOP)" ] # should be set by top Makefile...
	@headerlist="$(EXHEADER)"; for i in $$headerlist ; \
	do  \
	(cp $$i $(INSTALL_PREFIX)$(INSTALLTOP)/include/openssl/$$i; \
	chmod 644 $(INSTALL_PREFIX)$(INSTALLTOP)/include/openssl/$$i ); \
	done;

tags:
	ctags $(SRC)

lint:
	lint -DLINT $(INCLUDES) $(SRC)>fluff

update: depend

depend:
	$(MAKEDEPEND) -- $(CFLAG) $(INCLUDES) $(DEPFLAG) -- $(LIBSRC)

dclean:
	$(PERL) -pe 'if (/^# DO NOT DELETE THIS LINE/) {print; exit(0);}' $(MAKEFILE) >Makefile.new
	mv -f Makefile.new $(MAKEFILE)

clean:
	rm -f *.o *.obj lib tags core .pure .nfs* *.old *.bak fluff enc dec sign verify

# DO NOT DELETE THIS LINE -- make depend depends on it.
