include ../common.mak

CFLAGS	= -O2 -Wall
CFLAGS	+= -I$(SRCBASE)/include -I$(TOP)/shared -I$(TOP)/mssl
LDFLAGS	=

OBJS = mdu.o

all: mdu
	
mdu: $(OBJS)
	@echo " [mdu] CC -o $@"
	$(CC) $(LDFLAGS) -o $@ $^ -L../nvram -lnvram -L../shared -lshared -L../mssl -lmssl
#	$(CC) $(LDFLAGS) -o $@ $^ -L../nvram -lnvram -L../shared -lshared ../mssl/libmssl.a ../matrixssl/src/libmatrixsslstatic.a

	$(SIZECHECK)
	$(CPTMP)

clean:
	rm -f mdu .*.depend
	rm -f *.o

install: all
	@echo " [mdu] Installing..."
	install -D -m 0500 mdu $(INSTALLDIR)/bin/mdu
	$(STRIP) $(INSTALLDIR)/bin/mdu

%.o: %.c .%.depend
	@echo " [mdu] CC $@"
	@$(CC) $(CFLAGS) -c $<

.depend: $(OBJS:%.o=%.c)
	@$(CC) $(CFLAGS) -M $^ > .depend

.%.depend: %.c
	@$(CC) $(CFLAGS) -M $< > $@

-include $(OBJS:%.o=.%.depend)

