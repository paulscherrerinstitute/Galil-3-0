ifndef PSIMAKEFILE
PSIMAKEFILE=/ioc/tools/driver.makefile
endif

include $(PSIMAKEFILE)
include $(EPICS_MODULES)/makeUtils/latest/utils.mk


ifeq ($(findstring SL6,$(T_A)),SL6)

GNU_DIR = /opt/rh/devtoolset-7/root/usr
CC = $(GNU_BIN)/$(CMPLR_PREFIX)gcc
CCC = $(GNU_BIN)/$(CMPLR_PREFIX)g++

endif


EXCLUDE_VERSIONS=3.13 3.14.8 7.0.3
BUILDCLASSES=Linux
# Only build natively; cannot cross-build SL6 on RHEL7
# with current approach (just use devtoolset-7); the
# run-time libs are not backwards compatible! (I.e.,
# the product cannot be linked/loaded on a SL6 machine).
ARCH_FILTER=$(EPICS_HOST_ARCH)

USR_CXXFLAGS+=-std=c++11

USR_CXXFLAGS+= -D_GLIBCXX_USE_CXX11_ABI=0

TEMPLATES=$(wildcard ../Db/*.template)

ifndef INSTALL_DOC
INSTALL_DOC=$(MODULE_LOCATION)/doc
endif

mydbg:
	echo "INSTALLS: $(INSTALLS)"
	echo "DOCS: $(DOCS)"
	echo "RELEASE_TOPS: $(RELEASE_TOPS)"
	echo "TOP: $(TOP)"

ifdef INSTALL_MODULE_TOP_RULE
$(INSTALL_MODULE_TOP_RULE) install-doc-brute-force
endif

# Filenames with blanks are too painful.
# Just copy every time.
.PHONY: install-doc-brute-force

install-doc-brute-force:
	@echo "Installing Docs $@"
	$(MKDIR) $(INSTALL_DOC)
	for doc in ../../documentation/*.pdf ; do \
	echo "Installing $$doc"; \
	$(RM) "$(INSTALL_DOC)"/"`basename "$$doc"`" ;  \
	cp "$$doc" "$(INSTALL_DOC)"/ ; \
	done
	chmod 0444 "$(INSTALL_DOC)"/*

foo:
	echo "makeUtils_VERSION $(makeUtils_VERSION)"
	echo "makeUtils_VERSION_NUM $(makeUtils_VERSION_NUM)"
