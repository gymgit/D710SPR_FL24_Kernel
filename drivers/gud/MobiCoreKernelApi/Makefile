#
# this makefile is called from the kernel make syste
ifeq ($(MODE),release)
    EXTRA_CFLAGS+=-O2 -DNDEBUG
else  # DEBUG
    # "-O" is needed to expand inlines
    EXTRA_CFLAGS+=-O -g3 -DDEBUG
endif # DEBUG/RELEASE

ifdef MOBICORE_CFLAGS
    EXTRA_CFLAGS+=$(MOBICORE_CFLAGS)
endif

#Set the extra symbols
ifdef MCDRV_SYMBOLS_FILE
    KBUILD_EXTRA_SYMBOLS=$(MCDRV_SYMBOLS_FILE)
endif

#EXTRA_CFLAGS += -DDEBUG -DDEBUG_VERBOSE
EXTRA_CFLAGS += -Wno-declaration-after-statement
# add our module to kernel.
obj-m += mcKernelApi.o

mcKernelApi-objs := main.o clientlib.o device.o session.o connection.o

clean:
	rm -rf *.o *~ core .depend .*.cmd *.ko *.mod.c .tmp_versions \
		Module.markers Module.symvers modules.order

depend .depend dep:
	$(CC) $(CFLAGS) -M *.c > .depend

ifeq (.depend,$(wildcard .depend))
    include .depend
endif
