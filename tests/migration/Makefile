#
# Copyright (c) 2018 Red Hat, Inc. and/or its affiliates
#
# This work is licensed under the terms of the GNU GPL, version 2 or later.
# See the COPYING file in the top-level directory.
#

TARGET_LIST = i386 aarch64 s390x ppc64

SRC_PATH = ../..

.PHONY: help $(TARGET_LIST)
help:
	@echo "Create migration guest includes.  We generate a binary."
	@echo "And then convert that binary to an include file that can be"
	@echo "run in a guest."
	@echo "Possible operations are:"
	@echo
	@echo " $(MAKE) clean                Remove all intermediate files"
	@echo " $(MAKE) target               Generate for that target"
	@echo " $(MAKE) CROSS_PREFIX=... target"
	@echo "                              Cross-compile than target"
	@echo " Possible targets are: $(TARGET_LIST)"

override define __note
/* This file is automatically generated from the assembly file in
 * tests/migration/$@. Edit that file and then run "make all"
 * inside tests/migration to update, and then remember to send both
 * the header and the assembler differences in your patch submission.
 */
endef
export __note

$(TARGET_LIST):
	$(MAKE) CROSS_PREFIX=$(CROSS_PREFIX) -C $@

clean:
	for target in $(TARGET_LIST); do \
		$(MAKE) -C $$target clean; \
	done
