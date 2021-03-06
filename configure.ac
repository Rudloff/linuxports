dnl Process this file with autoconf to produce a configure script.
dnl $Id$
AC_PREREQ(2.63)
AC_DEFUN([MACPORTS_VERSION_MACRO], [esyscmd(<config/macports_version tr -d '\n')])
AC_INIT([MacPorts],MACPORTS_VERSION_MACRO,[macports-dev@lists.macosforge.org],[macports])
AC_CONFIG_SRCDIR([src/pextlib1.0/Pextlib.c])
AC_CONFIG_HEADERS([src/config.h])

AC_CANONICAL_TARGET

# Read in the MacPorts version from the base/config/macports_version file
AC_MSG_CHECKING(MacPorts version)
MACPORTS_VERSION=MACPORTS_VERSION_MACRO
AC_MSG_RESULT([$MACPORTS_VERSION])
AC_SUBST(MACPORTS_VERSION)

# Check user PATH for MP paths, and remove as necessary.
MP_PATH_SCAN
MP_FLAGS_SCAN

AC_PATH_PROG(SW_VERS, sw_vers)
AC_PATH_PROG(DEFAULTS, defaults)
AC_PATH_PROG(XCODE_SELECT, xcode-select)

if test "x$SW_VERS" != "x"; then
  AC_MSG_CHECKING(Mac OS X version)
  MACOSX_VERSION=`$SW_VERS -productVersion`
  AC_MSG_RESULT([$MACOSX_VERSION])
fi

case "$MACOSX_VERSION" in
  10.0*|10.1|10.1.*|10.2*|10.3*)
    AC_MSG_ERROR([This version of Mac OS X is not supported
                  Please upgrade at http://store.apple.com/])
    ;;
  10.4.[[0-9]]|10.4.10|10.5.[[0-7]]|10.6.[[0-7]]|10.7.[[0-4]]|10.8.[[0-4]])
    AC_MSG_WARN([This version of Mac OS X is out of date])
    AC_MSG_WARN([Please run Software Update to update it])
    ;;
  10.4*|10.5*|10.6*|10.7*|10.8*|10.9*)
    dnl Supported version
    ;;
  *)
    ;;
esac

# locate currently selected Xcode path
AC_MSG_CHECKING(Xcode location)
if test "x$XCODE_SELECT" != "x"; then
  DEVELOPER_DIR=`$XCODE_SELECT -print-path`
fi
if test -z "$DEVELOPER_DIR" -o ! -d "$DEVELOPER_DIR" ; then
    if test -d /Applications/Xcode.app/Contents/Developer ; then
        DEVELOPER_DIR=/Applications/Xcode.app/Contents/Developer
    else
        DEVELOPER_DIR=/Developer
    fi
fi
AC_MSG_RESULT([$DEVELOPER_DIR])
AC_SUBST(DEVELOPER_DIR)

case "$DEVELOPER_DIR" in
  *Xcode.app/Contents/Developer)
    XCODEPLIST_BASE=`dirname $DEVELOPER_DIR`/version
    ;;
  *)
    XCODEPLIST_BASE=$DEVELOPER_DIR/Applications/Xcode.app/Contents/version
    ;;
esac
XCODEPLIST=${XCODEPLIST_BASE}.plist
if test -r "$XCODEPLIST"; then
  AC_MSG_CHECKING(Xcode version)
  if test "x$DEFAULTS" != "x"; then
    XCODE_VERSION=`$DEFAULTS read $XCODEPLIST_BASE CFBundleShortVersionString`
  else
    XCODE_VERSION=`tr -d '\r\n' < $XCODEPLIST | sed -e 's/.*<key>CFBundleShortVersionString<\/key>.<string>\([[0-9.]]*\)<\/string>.*/\1/'`
  fi
  AC_MSG_RESULT([$XCODE_VERSION])
fi

case "$XCODE_VERSION" in
  1.*|2.[[0-1]]*)
    AC_MSG_WARN([This version of Xcode Tools is not supported])
    AC_MSG_WARN([Please upgrade at https://developer.apple.com/downloads/])
    ;;
  2.[[2-3]]*|3.[[0]]*)
    AC_MSG_WARN([This version of Xcode Tools is out of date])
    AC_MSG_WARN([Please consider upgrading as some ports fail compiling])
    ;;
  2.*|3.*|4.*|5.*)
    dnl Supported version
    ;;
  *)
    ;;
esac

# Checks for programs.
AC_PROG_CC([clang cc gcc])
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET
AC_PROG_OBJC([clang cc gcc])

AC_PATH_PROGS(BSDMAKE, [bsdmake pmake], [])
AC_PATH_PROG(BZIP2, [bzip2], [])
AC_PATH_PROG(BZR, [bzr], [])
AC_PATH_PROG(CHOWN, [chown], [], [$PATH:/usr/sbin])
AC_PATH_PROG(CP, [cp], [])
AC_PATH_PROG(CPIO, [cpio], [])
AC_PATH_PROG(CVS, [cvs], [])
AC_PATH_PROG(DIFF, [diff], [])
AC_PATH_PROG(DSCL, [dscl], [])
AC_PATH_PROG(DSEDITGROUP, [dseditgroup], [], [$PATH:/usr/sbin])
AC_PATH_PROG(FILE, [file], [])
AC_PATH_PROG(FIND, [find], [])
AC_PATH_PROG(GIT, [git], [])
AC_PATH_PROGS(GNUMAKE, [gnumake gmake], [])
AC_PATH_PROGS(GNUPATCH, [gnupatch gpatch], [])
AC_PATH_PROGS(GNUTAR, [gnutar gtar], [])
AC_PATH_PROG(GZIP, [gzip], [])
AC_PATH_PROG(HDIUTIL, [hdiutil], [])
AC_PATH_PROG(HG, [hg], [])
AC_PATH_PROG(LAUNCHCTL, [launchctl], [])
AC_PATH_PROG(LIPO, [lipo], [])
AC_PATH_PROG(LSBOM, [lsbom], [])
AC_PATH_PROG(LZMA, [lzma], [])
AC_PATH_PROG(MAKE, [make])
AC_PATH_PROG(MDFIND, [mdfind], [])
AC_PATH_PROG(MDLS, [mdls], [])
AC_PATH_PROG(MKBOM, [mkbom], [])
AC_PATH_PROGS(MTREE, [mtree fmtree freebsd-mtree], [], [$PATH:/usr/sbin])
AC_PATH_PROG(OPEN, [open], [])
AC_PATH_PROG(OPENSSL, [openssl], [])
AC_PATH_PROG(PATCH, [patch], [])
AC_PATH_PROG(PAX, [pax], [])
AC_PATH_PROG(RMDIR, [rmdir], [])
AC_PATH_PROG(RSYNC, [rsync], [])
AC_PATH_PROG(SANDBOX_EXEC, [sandbox-exec], [], [/usr/bin])
AC_PATH_PROG(SED, [sed])
AC_PATH_PROG(SVN, [svn], [])
AC_PATH_PROG(SWIG, [swig], [])
AC_PATH_PROG(TAR, [tar])
AC_PATH_PROG(UNZIP, [unzip])
AC_PATH_PROG(XAR, [xar], [])
AC_PATH_PROG(XCODEBUILD, [xcodebuild], [])
AC_PATH_PROG(XCRUN, [xcrun], [])
AC_PATH_PROG(XZ, [xz], [])
AC_PATH_PROG(ZIP, [zip])

AC_CHECK_PROG(HAVE_LAUNCHD, [launchd], [yes], [], [/sbin])

# Define some precious variables allowing user to override PATH for some programs
AC_ARG_VAR(BSDMAKE, [path to bsdmake/pmake command])
AC_ARG_VAR(BZIP2, [path to bzip2 command])
AC_ARG_VAR(CVS, [path to cvs command])
AC_ARG_VAR(GNUMAKE, [path to gnumake command])
AC_ARG_VAR(GNUTAR, [path to gnutar command])
AC_ARG_VAR(LZMA, [path to lzma command])
AC_ARG_VAR(MAKE, [path to make command])
AC_ARG_VAR(MTREE, [path to mtree command])
AC_ARG_VAR(OPEN, [path to open command])
AC_ARG_VAR(OPENSSL, [path to openssl command])
AC_ARG_VAR(RSYNC, [path to rsync command])
AC_ARG_VAR(SED, [path to sed command])
AC_ARG_VAR(SVN, [path to svn command])
AC_ARG_VAR(SWIG, [path to swig command])
AC_ARG_VAR(TAR, [path to tar command])
AC_ARG_VAR(XAR, [path to xar command])
AC_ARG_VAR(XZ, [path to xz command])

if test "x$MTREE" = "x"; then
    AC_MSG_ERROR([mtree not found])
fi

MP_SED_EXTENDED_REGEXP
MP_TAR_FAST_READ
MP_TAR_NO_SAME_OWNER
MP_PATCH_GNU_VERSION

# Quiche eaters options.
if test x$GCC = xyes; then
	CFLAGS_QUICHEEATERS='-Wextra -Wall'
	CFLAGS_PEDANTIC='-pedantic'
fi
AC_SUBST(CFLAGS_QUICHEEATERS)
AC_SUBST(CFLAGS_PEDANTIC)
MP_WERROR

MP_COMPILER_ATTRIBUTE_UNUSED
MP_COMPILER_ATTRIBUTE_LF_PRIVATE

# Foundation checks
ACX_PTHREAD
MP_OBJC_RUNTIME
MP_OBJC_FOUNDATION

MP_PROG_DAEMONDO

AC_SUBST(EXTRA_PROGS)

# set default ports-directory
PORTS_DIR_DEFAULT=`pwd | sed -e "s/base/ports/"`

# Check for paths
AC_PREFIX_DEFAULT(/opt/local)
AC_ARG_WITH(
		unsupported-prefix,
		AS_HELP_STRING([--with-unsupported-prefix],
		[Acknowledge that you accept the consequences of using an unsupported prefix.]),
		[with_unsupported_prefix=$withval],
		[with_unsupported_prefix=no])
if test x$prefix = x/usr/local -o x$prefix = x/usr && test x$with_unsupported_prefix != xyes; then
    AC_MSG_ERROR([Installing MacPorts into $prefix is not supported. If \
you understand this and wish to do so anyway, pass --with-unsupported-prefix \
to configure.])
fi
MP_PATH_PORTSDIR([$PORTS_DIR_DEFAULT])
MP_PATH_MPCONFIGDIR

# Check whether to install without root privileges
MP_CHECK_NOROOTPRIVILEGES

# Check for install ownership
MP_CHECK_INSTALLUSER
MP_CHECK_INSTALLGROUP
MP_CHECK_RUNUSER
MP_DIRECTORY_MODE
MP_SHARED_DIRECTORY

# Check for default directories
MP_PATH_APPLICATIONS
MP_PATH_FRAMEWORKS

# Check for universal options
MP_UNIVERSAL_OPTIONS

# Check for standard header files.
AC_HEADER_STDC
AC_HEADER_DIRENT
AC_HEADER_SYS_WAIT
AC_CHECK_HEADERS([crt_externs.h err.h fcntl.h libkern/OSAtomic.h limits.h paths.h pwd.h \
	readline/history.h readline/readline.h spawn.h sys/cdefs.h sys/event.h sys/fcntl.h sys/file.h \
	sys/paths.h sys/socket.h sys/sysctl.h utime.h])

# Checks for library functions.
AC_CHECK_FUNCS([OSAtomicCompareAndSwap32 OSAtomicCompareAndSwap64 \
	OSAtomicCompareAndSwapPtr __getdirentries64 bzero clearenv copyfile fgetln \
	flock fls kqueue lockf memset posix_spawn setmode strcasecmp strlcat \
	strlcpy strncasecmp sysctlbyname])
AC_SUBST([ac_cv_func_strlcat])

MP_CHECK_READLINK_IS_P1003_1A

# Check for md5 implementation
AC_CHECK_HEADER([CommonCrypto/CommonDigest.h], [AC_DEFINE([HAVE_COMMONCRYPTO_COMMONDIGEST_H], [1], [Define if CommonCrypto is available.])], [MP_LIB_MD5])

# Check for readline
AC_ARG_ENABLE(readline, AS_HELP_STRING([--enable-readline],[Enable addition of readline support, if readline present.]),
[
	AC_CHECK_LIB([readline], [readline], [
				  READLINE_LIBS=-lreadline
				  AC_DEFINE([HAVE_LIBREADLINE], [1], [Define to 1 if you have the 'readline' library (-lreadline).])
				  ])
	AC_CHECK_DECLS([rl_username_completion_function,rl_filename_completion_function,rl_completion_matches,username_completion_function,filename_completion_function,completion_matches], [], [],
	[
	#include <stdio.h>
	#if HAVE_READLINE_READLINE_H
	# include <readline/readline.h>
	#endif
	])
])
AC_SUBST(READLINE_LIBS)

# Lowest non-system-reserved uid and gid (Apple claims <500)
AC_DEFINE([MIN_USABLE_UID], [500], [Lowest non-system-reserved UID.])
AC_DEFINE([MIN_USABLE_GID], [500], [Lowest non-system-reserved GID.])

# Substitute platform for base compatibility check
MP_PLATFORM

## libcurl
MP_LIBCURL_FLAGS

## sqlite3
MP_SQLITE3_FLAGS

MP_CHECK_SQLITE_VERSION(3003011)
if test "x${mp_sqlite_version_ge_3003011}" = "xno"; then
	AC_DEFINE([sqlite3_prepare_v2], [sqlite3_prepare], [define sqlite3_prepare to sqlite_prepare_v2 if the latter is not available])
fi

# check whether trace mode is supported on this platform
MP_TRACEMODE_SUPPORT

# misc variables that need to be expanded for substitution into tcl
oldprefix=$prefix
oldexec_prefix=$exec_prefix
if test "x$prefix" = "xNONE" ; then
   prefix=$ac_default_prefix
fi
if test "x$exec_prefix" = "xNONE" ; then
	exec_prefix=$prefix
fi
eval "prefix_expanded=$prefix"
eval "exec_prefix_expanded=$exec_prefix"
AC_SUBST(prefix_expanded)
# do this twice, since there is a nested variable of
# ${prefix} inside of ${sysconfdir}
eval "MPCONFIGDIR_EXPANDED=$MPCONFIGDIR"
eval "MPCONFIGDIR_EXPANDED=$MPCONFIGDIR_EXPANDED"
AC_SUBST(MPCONFIGDIR_EXPANDED)
eval "localstatedir_expanded=$localstatedir"
AC_SUBST(localstatedir_expanded)
# Compute the libexec dir for the vendor packages
eval "macports_libexec_dir=${libexecdir}/macports"
eval "macports_libexec_dir=$macports_libexec_dir"
prefix=$oldprefix
exec_prefix=$oldexec_prefix

# Determine if we need to install some bundled packages
VENDOR_PACKAGES=

## Tcl package
tcl_version=8.5.15
tcl_thread_version=2.7.0
tcllib_version=1.15
MP_CONFIG_TARBALL([vendor/tcl${tcl_version}-src.tar.gz], [vendor/tcl${tcl_version}/unix], [--prefix=${macports_libexec_dir} --enable-threads])
VENDOR_TCL_SUBDIR=tcl${tcl_version}/unix
VENDOR_TCL_INSTALL="install-binaries install-libraries"
AC_SUBST(VENDOR_TCL_SUBDIR)
AC_SUBST(VENDOR_TCL_INSTALL)

# Set up some variables needed by MacPorts' Tcl setup
VENDOR_DESTROOT=vendor/vendor-destroot
AC_SUBST(VENDOR_DESTROOT)

## Tcl Thread package
# Tcl supports Threads internally, but to use threads from Tcl code we need
# this package
MP_CONFIG_TARBALL([vendor/thread${tcl_thread_version}.tar.gz], [vendor/thread${tcl_thread_version}], [--prefix=${macports_libexec_dir}])
VENDOR_TCLTHREAD_SUBDIR=thread${tcl_thread_version}
VENDOR_TCLTHREAD_INSTALL="install-binaries install-libraries"
AC_SUBST(VENDOR_TCLTHREAD_SUBDIR)
AC_SUBST(VENDOR_TCLTHREAD_INSTALL)

## Tcllib package
# Note that Tcllib needs a Tcl interpreter during installation; it will *not*
# be the one we configure above, because that one isn't built yet. That's not
# a problem, though -- it's only used during installation.
MP_CONFIG_TARBALL([vendor/tcllib-${tcllib_version}.tar.gz], [vendor/tcllib-${tcllib_version}], [--prefix=${macports_libexec_dir}])
VENDOR_PACKAGES="$VENDOR_PACKAGES tcllib-${tcllib_version}"
VENDOR_TCLLIB_SUBDIR=tcllib-${tcllib_version}
VENDOR_TCLLIB_INSTALL="install-libraries"
AC_SUBST(VENDOR_TCLLIB_SUBDIR)
AC_SUBST(VENDOR_TCLLIB_INSTALL)

# Load tclConfig.sh from our private install of Tcl
AC_MSG_CHECKING([for Tcl configuration])
TCL_BIN_DIR=`(cd vendor/tcl${tcl_version}/unix; pwd)`
AC_MSG_RESULT([found $TCL_BIN_DIR/tclConfig.sh])
SC_LOAD_TCLCONFIG
SC_ENABLE_SHARED

# Pull compiler/linker values from tclConfig.sh
SHLIB_LD=${TCL_SHLIB_LD}
STLIB_LD=${TCL_STLIB_LD}
SHLIB_CFLAGS=${TCL_SHLIB_CFLAGS}
SHLIB_SUFFIX=${TCL_SHLIB_SUFFIX}
TCLSH=${TCL_EXEC_PREFIX}/bin/tclsh${TCL_VERSION}
INTREE_TCLSH=${TCL_BIN_DIR}/tclsh
# strip possible whitespace at the end of TCL_PACKAGE_PATH
eval "TCL_PACKAGE_PATH=${TCL_PACKAGE_PATH}"

AC_SUBST(SHLIB_LD)
AC_SUBST(STLIB_LD)
AC_SUBST(SHLIB_CFLAGS)
AC_SUBST(SHLIB_SUFFIX)
AC_SUBST(TCL_PREFIX)
AC_SUBST(TCL_VERSION)
AC_SUBST(TCL_PACKAGE_PATH)
AC_SUBST(TCL_STUB_LIB_SPEC)
AC_SUBST(TCL_SRC_DIR)
AC_SUBST(TCLSH)
AC_SUBST(INTREE_TCLSH)

INCLUDES="-I.. -I. $INCLUDES"
AC_SUBST(INCLUDES)

# Check if there's an existing DP/MP install too old to upgrade
MP_CHECK_OLDLAYOUT

# Output
AC_CONFIG_FILES([
	Doxyfile
	Makefile
	Mk/macports.autoconf.mk
	doc/Makefile
	doc/base.mtree
	doc/macosx.mtree
	doc/macports.conf
	doc/prefix.mtree
	doc/pubkeys.conf
	portmgr/freebsd/Makefile
	portmgr/dmg/postflight
	setupenv.bash
	src/Makefile
	src/cflib1.0/Makefile
	src/cregistry/Makefile
	src/darwintracelib1.0/Makefile
	src/machista1.0/Makefile
	src/macports1.0/Makefile
	src/macports1.0/macports_autoconf.tcl
	src/macports1.0/macports_test_autoconf.tcl
	src/package1.0/Makefile
	src/package1.0/package_test_autoconf.tcl
	src/pextlib1.0/Makefile
	src/port/Makefile
	src/port1.0/Makefile
	src/port1.0/port_autoconf.tcl
	src/port1.0/port_test_autoconf.tcl
	src/programs/Makefile
	src/registry2.0/Makefile
	src/registry2.0/registry_autoconf.tcl
	tests/Makefile
	tests/test.tcl
	vendor/Makefile
])

AC_CONFIG_FILES([src/dedup_portfiles.tcl], [chmod +x src/dedup_portfiles.tcl])
AC_CONFIG_FILES([src/images_to_archives.tcl], [chmod +x src/images_to_archives.tcl])
AC_CONFIG_FILES([src/pkg_mkindex.sh], [chmod +x src/pkg_mkindex.sh])
AC_CONFIG_FILES([src/upgrade_sources_conf_default.tcl], [chmod +x src/upgrade_sources_conf_default.tcl])

AC_OUTPUT
