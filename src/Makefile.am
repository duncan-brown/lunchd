pkglocalstatedir = $(localstatedir)/lunchd
execlaunchddir = @launchddir@

sbin_SCRIPTS = lunchd
pkgdata_DATA = lunchd-addresses.txt lunchd-destinations.csv
pkglocalstate_DATA = lunchd-history.log
EXTRA_DIST = lunchd.in lunchd.cron.in lunchd.plist.in lunchd-addresses.txt lunchd-destinations.csv
CLEANFILES = lunchd-history.log

if OS_DARWIN
execlaunchd_DATA = lunchd.plist
endif

lunchd-history.log:
	touch $@

install-data-local:
	@if test -f "$(DESTDIR)$(pkgdatadir)/lunchd-addresses.txt" ; then mv "$(DESTDIR)$(pkgdatadir)/lunchd-addresses.txt" "$(DESTDIR)$(pkgdatadir)/lunchd-addresses.txt.bak" ; echo "WARNING: saved old address file $(DESTDIR)$(pkgdatadir)/lunchd-addresses.txt as $(DESTDIR)$(pkgdatadir)/lunchd-addresses.txt.bak" ; fi
	@if test -f "$(DESTDIR)$(pkgdatadir)/lunchd-destinations.csv" ; then mv "$(DESTDIR)$(pkgdatadir)/lunchd-destinations.csv" "$(DESTDIR)$(pkgdatadir)/lunchd-destinations.csv.bak" ; echo "WARNING: saved old address file $(DESTDIR)$(pkgdatadir)/lunchd-destinations.csv as $(DESTDIR)$(pkgdatadir)/lunchd-destinations.csv.bak" ; fi

if OS_DARWIN
install-exec-hook:
	@echo "launching lunchd"
	-launchctl remove edu.uwmlsc.lunchd
	launchctl load $(DESTDIR)$(launchddir)/lunchd.plist
uninstall-local:
	@echo "unlaunching lunchd"
	-launchctl remove edu.uwmlsc.lunchd
else
install-exec-hook:
	@echo "adding lunchd to the crontab"
	rm -f /tmp/lunchd-crontab.tmp
	crontab -l | sed '/lunchd/d' > /tmp/lunchd-crontab.tmp
	cat lunchd.cron >> /tmp/lunchd-crontab.tmp 
	crontab /tmp/lunchd-crontab.tmp
	rm -f /tmp/lunchd-crontab.tmp
uninstall-local:
	@echo "removing lunchd from the crontab"
	rm -f /tmp/lunchd-crontab.tmp
	crontab -l | sed '/lunchd/d' > /tmp/lunchd-crontab.tmp
	crontab /tmp/lunchd-crontab.tmp
	rm -f /tmp/lunchd-crontab.tmp
endif
