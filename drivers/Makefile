##############################################################################
##
##  This file is part of the Chaos Kernel, and is made available under
##  the terms of the GNU General Public License version 2.
##
##  Copyright (C) 2017 - Benjamin Grange <benjamin.grange@epitech.eu>
##
##############################################################################

SRC_C += $(wildcard *.c)
SRC_ASM += $(wildcard *.asm)

OBJS += $(SRC_C:.c=.o) $(SRC_ASM:.asm=.o)
DEPS = $(OBJS:.o=.d)

DRIVER_OBJ = drivers.o

.PHONY: all
all: $(DRIVER_OBJ)

$(DRIVER_OBJ): $(OBJS)
	$(Q)printf "  LD\t $@\n"
	$(Q)$(LD) $(LDFLAGS) -o $@ -r $^

.PHONY: clean
clean:
	$(Q)$(RM) $(DRIVER_OBJ) $(OBJS) $(DEPS)

-include $(DEPS)
%.o: %.c
	$(Q)printf "  CC\t $<\n"
	$(Q)$(CC) $(CFLAGS) -c $< -o $@

-include $(DEPS)
%.o: %.asm
	$(Q)printf "  NASM\t $<\n"
	$(Q)$(NASM) $(NASMFLAGS) -M $< -o $@ > $(patsubst %.o,%.d, $@)
	$(Q)$(NASM) $(NASMFLAGS) $< -o $@
