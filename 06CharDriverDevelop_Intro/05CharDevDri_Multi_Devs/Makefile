MODNAME = firstchardevdriver
CROSS_COMPILE = arm-linux-
TESTPRE = test

ifeq ($(PLATFORM),PC)
KERNELDIR ?= /lib/modules/$(shell uname -r)/build
else
CC = $(CROSS_COMPILE)gcc 
KERNELDIR ?= /opt/real6410/kernel/linux-2.6.28.6
endif

obj-m := $(MODNAME).o

default: test driver

test:	
	@echo "Compiling test program..."
	$(CC) $(TESTPRE)$(MODNAME)0.c -o $(TESTPRE)$(MODNAME)0
	$(CC) $(TESTPRE)$(MODNAME)1.c -o $(TESTPRE)$(MODNAME)1
	@echo
driver:
	@echo "Compiling device driver..."
	$(MAKE) -C $(KERNELDIR) M=$(PWD) modules
	@echo
clean:
	@echo "Clean test proigram..."
	@rm -rf $(TESTPRE)$(MODNAME)0 $(TESTPRE)$(MODNAME)1
	@echo
	@echo "Clean device driver..."
	@rm -rf *.o *.ko *.mod.* .$(MODNAME).* .tmp* Module* module*
	@echo
copy:
	@cp *.ko /opt/nfsroot/lib/modules/2.6.28.6/kernel/drivers/