# The rhn-client-tools Makefiles might not be set up in the smartest way. This
# Makefile doesn't worry about anything outside of this directory even if these
# files need them, such as the glade files. Be sure to run make in 
# rhn-client-tools and not here.

FILES		:= config gui hardware progress \
		   haltree hardware_hal hardware_gudev \
		   up2dateUtils getMethod tui \
		   up2dateLog rpmUtils rhnreg transaction \
		   up2dateErrors rpcServer up2dateAuth \
		   rhnPackageInfo rhnChannel \
		   rhnHardware \
		   clientCaps capabilities \
		   rhnregGui rhnserver \
		   messageWindow rhncli \
		   rhnreg_constants \
                   pkgplatform debUtils pkgUtils \
                   pmPlugin

PYFILES 	:= $(addsuffix .py, $(FILES))
INITFILE	:= __init__.py
OBJECTS		:= $(PYFILES)

PYCHECKER       := /usr/bin/pychecker

RHNSHARE_DIR	:= $(PREFIX)/usr/share/rhn

INSTALL         := install -p --verbose 
INSTALL_DIR     := $(INSTALL) -m 755 -d 
INSTALL_DATA    = $(INSTALL) -m 644 

all:: $(OBJECTS)

install:: all
	$(INSTALL_DATA) $(PYFILES) $(INITFILE) $(RHNSHARE_DIR)/up2date_client

	$(INSTALL_DATA) $(INITFILE) $(RHNSHARE_DIR)/

	# this is lame and should be dealt with in the code
	sed -i -e "s|\@VERSION\@|$(VERSION)|" \
		$(RHNSHARE_DIR)/up2date_client/up2dateUtils.py
	sed -i -e "s|\@PLATFORM\@|$(PLATFORM)|" \
		$(RHNSHARE_DIR)/up2date_client/pkgplatform.py

# OTHER targets for internal use
pychecker:: 
	@$(PYCHECKER) $(PYFILES) || exit 0
graphviz:: 
	@$(PYCHECKER) -Z $(PYFILES) || exit 0

clean::
	@rm -fv *.pyc *~ .*~
