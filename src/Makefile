obj-m := dattobd.o

KERNELVERSION = $(shell uname -r)
KDIR := /lib/modules/$(KERNELVERSION)/build
PWD := $(shell pwd)
EXTRA_CFLAGS := -g
default:
	if [ ! -f kernel-config.h ] || tail -1 kernel-config.h | grep -qv '#endif'; then ./genconfig.sh $(KERNELVERSION); fi;
	$(MAKE) -I/usr/include -C $(KDIR) SUBDIRS=$(PWD) modules
	
clean:
	$(MAKE) -I/usr/include -C $(KDIR) SUBDIRS=$(PWD) clean
	rm -f kernel-config.h

insmod: default
	insmod dattobd.ko
	
rmmod:
	rmmod dattobd
