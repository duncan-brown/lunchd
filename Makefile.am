SUBDIRS = src
vcs-clean: maintainer-clean
	rm -f Makefile.in aclocal.m4 configure src/Makefile.in
install-data-local:
	@echo "";\
	echo "=================================================================";\
	echo "";\
	echo "	Lunchd has been installed -- please edit the files";\
	echo "";\
	echo "		$(DESTDIR)$(datadir)/lunchd/lunchd-addresses.txt";\
	echo "		$(DESTDIR)$(datadir)/lunchd/lunchd-destinations.csv";\
	echo "";\
	echo "================================================================="
