AC_INIT([lunchd],[1.0],[jolien@gravity.phys.uwm.edu])
AC_CONFIG_SRCDIR([configure.ac])
AC_CONFIG_AUX_DIR([aux])
AC_CONFIG_FILES([Makefile])
AC_CONFIG_FILES([src/Makefile])
AC_CONFIG_FILES([src/lunchd], [chmod +x src/lunchd])
AC_CONFIG_FILES([src/lunchd.cron])
AC_CONFIG_FILES([src/lunchd.plist])
AM_INIT_AUTOMAKE([foreign])
AC_CANONICAL_HOST
case "${host_os}" in
	darwin*) lunchd_host_os="darwin";;
	linux*)  lunchd_host_os="linux";;
	*)       lunchd_host_os="unknown";;
esac
if test "${lunchd_host_os}" = "darwin" ; then
	if test "${UID}" = "0" ; then
		launchddir="/Library/LaunchDaemons"
	else
		launchddir="${HOME}/Library/LaunchAgents"
	fi
else
	launchddir=
fi
AC_SUBST(launchddir)
AM_CONDITIONAL(OS_DARWIN, test "${lunchd_host_os}" = "darwin")
AM_CONDITIONAL(OS_LINUX, test "${lunchd_host_os}" = "linux")
AC_PROG_AWK
AC_PATH_PROG([SENDMAIL], [sendmail], AC_MSG_ERROR([cannot find the sendmail program]), [/usr/sbin])
AC_ARG_VAR([AWK], [awk program])
AC_ARG_VAR([SENDMAIL], [sendmail program])
AC_OUTPUT
cat <<EOF
================================================================

	Lunchd has been configured.

	To UPGRADE an exising installation of lunchd while
	keeping the exising destinations and addresses, run

		make install-exec
	
	To INSTALL new address and destination files, run

		make install-data

	To do both, run

		make install

	Lunchd will be installed under the directory

		$prefix

=================================================================
EOF
