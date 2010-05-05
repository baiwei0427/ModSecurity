dnl
dnl Autoconf configuration for ModSecurity
dnl
dnl     Use ./autogen.sh to produce a configure script
dnl

AC_PREREQ(2.63)

AC_INIT([modsecurity], [2.5], [support@modsecurity.org])

AC_CONFIG_MACRO_DIR([acinclude])
AC_CONFIG_SRCDIR([LICENSE])
AC_CONFIG_HEADERS([modsecurity_config.h])
AC_CONFIG_AUX_DIR([build])

AM_INIT_AUTOMAKE([-Wall -Werror foreign])

LT_PREREQ([2.2])
LT_INIT([dlopen])

# Checks for programs.
AC_PROG_AWK
AC_PROG_CC
AC_PROG_CPP
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET
AC_PROG_GREP
AC_PATH_PROGS(PERL, [perl perl5], )
AC_PATH_PROGS(ENV_CMD, [env printenv], )

# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([fcntl.h limits.h stdlib.h string.h unistd.h sys/types.h sys/stat.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_C_INLINE
AC_C_RESTRICT
AC_TYPE_PID_T
AC_TYPE_SIZE_T
AC_STRUCT_TM
AC_TYPE_UINT8_T

# Checks for library functions.
AC_FUNC_MALLOC
AC_FUNC_MEMCMP
AC_CHECK_FUNCS([atexit getcwd memmove memset strcasecmp strchr strdup strerror strncasecmp strrchr strstr strtol fchmod])

# Some directories
MSC_BASE_DIR=`pwd`
MSC_PKGBASE_DIR="$MSC_BASE_DIR/.."
MSC_TEST_DIR="$MSC_BASE_DIR/tests"
MSC_REGRESSION_DIR="$MSC_TEST_DIR/regression"
MSC_REGRESSION_SERVERROOT_DIR="$MSC_REGRESSION_DIR/server_root"
MSC_REGRESSION_CONF_DIR="$MSC_REGRESSION_SERVERROOT_DIR/conf"
MSC_REGRESSION_LOGS_DIR="$MSC_REGRESSION_SERVERROOT_DIR/logs"
MSC_REGRESSION_DOCROOT_DIR="$MSC_REGRESSION_SERVERROOT_DIR/htdocs"

AC_SUBST(MSC_BASE_DIR)
AC_SUBST(MSC_PKGBASE_DIR)
AC_SUBST(MSC_TEST_DIR)
AC_SUBST(MSC_REGRESSION_DIR)
AC_SUBST(MSC_REGRESSION_SERVERROOT_DIR)
AC_SUBST(MSC_REGRESSION_CONF_DIR)
AC_SUBST(MSC_REGRESSION_LOGS_DIR)
AC_SUBST(MSC_REGRESSION_DOCROOT_DIR)

### Configure Options

TOPLEVEL_SUBDIRS="tools"

# Apache2 Module
AC_ARG_ENABLE(apache2-module,
              AS_HELP_STRING([--disable-apache2-module],
                             [Disable building Apache2 module.]),
[
  if test "$enableval" != "no"; then
    build_apache2_module=1
  else
    build_apache2_module=0
  fi
],
[
  build_apache2_module=1
])
AM_CONDITIONAL([BUILD_APACHE2_MODULE], [test "$build_apache2_module" -eq 1])
if test "$build_apache2_module" -eq 1; then
  TOPLEVEL_SUBDIRS="$TOPLEVEL_SUBDIRS apache2"
fi


# Extensions
AC_ARG_ENABLE(extentions,
              AS_HELP_STRING([--enable-extentions],
                             [Enable building extension.]),
[
  if test "$enableval" != "no"; then
    build_extentions=1
  else
    build_extentions=0
  fi
],
[
  build_extentions=0
])
AM_CONDITIONAL([BUILD_extentions], [test "$build_extentions" -eq 1])
if test "$build_extentions" -eq 1; then
  TOPLEVEL_SUBDIRS="$TOPLEVEL_SUBDIRS ext"
fi


# Mlogc
AC_ARG_ENABLE(mlogc,
              AS_HELP_STRING([--disable-mlogc],
                             [Disable building mlogc.]),
[
  if test "$enableval" != "no"; then
    build_mlogc=1
  else
    build_mlogc=0
  fi
],
[
  build_mlogc=1
])
AM_CONDITIONAL([BUILD_MLOGC], [test "$build_mlogc" -eq 1])
if test "$build_mlogc" -eq 1; then
  TOPLEVEL_SUBDIRS="$TOPLEVEL_SUBDIRS mlogc"
fi

# Documentation
AC_ARG_ENABLE(docs,
              AS_HELP_STRING([--enable-docs],
                             [Enable building documentation.]),
[
  if test "$enableval" != "no"; then
    build_docs=1
  else
    build_docs=0
  fi
],
[
  build_docs=0
])
AM_CONDITIONAL([BUILD_DOCS], [test "$build_docs" -eq 1])
if test "$build_docs" -eq 1; then
    TOPLEVEL_SUBDIRS="$TOPLEVEL_SUBDIRS docs"
fi


# Add PCRE Studying

AC_ARG_ENABLE(pcre-study,
              AS_HELP_STRING([--enable-pcre-study],
                             [Enable PCRE regex studying during configure.]),
[
  if test "$enableval" != "no"; then
    pcre_study='-DWITH_PCRE_STUDY'
  else
    pcre_study=''
  fi
],
[
  pcre_study='-DWITH_PCRE_STUDY'
])

# Limit PCRE matching
AC_ARG_ENABLE(pcre-match-limit,
              AS_HELP_STRING([--enable-pcre-match-limit],
                             [Enable PCRE regex match limit during configure.]),
[
  if test "$enableval" = "yes"; then
    AC_MSG_ERROR([PCRE match limits require a numeric value])
  elif test "$enableval" = "no"; then
    pcre_match_limit=''
  else
    pcre_match_limit="-DMODSEC_PCRE_MATCH_LIMIT=$enableval"
  fi
],
[
  pcre_match_limit='-DMODSEC_PCRE_MATCH_LIMIT=1500'
])

# Limit PCRE matching recursion
AC_ARG_ENABLE(pcre-match-limit-recursion,
              AS_HELP_STRING([--enable-pcre-match-limit-recursion],
                             [Enable PCRE regex match limit recursion during configure.]),
[
  if test "$enableval" = "yes"; then
    AC_MSG_ERROR([PCRE match limits require a numeric value])
  elif test "$enableval" = "no"; then
    pcre_match_limit_recursion=''
  else
    pcre_match_limit_recursion="-DMODSEC_PCRE_MATCH_LIMIT_RECURSION=$enableval"
  fi
],
[
  pcre_match_limit_recursion='-DMODSEC_PCRE_MATCH_LIMIT_RECURSION=1500'
])

# Ignore configure errors
AC_ARG_ENABLE(errors,
              AS_HELP_STRING([--disable-errors],
                             [Disable errors during configure.]),
[
  if test "$enableval" != "no"; then
    report_errors=1
  else
    report_errors=0
  fi
],
[
  report_errors=1
])

# Verbose output
AC_ARG_ENABLE(verbose-output,
              AS_HELP_STRING([--enable-verbose-output],
                             [Enable more verbose configure output.]),
[
  if test "$enableval" != "no"; then
    verbose_output=1
  else
    verbose_output=0
  fi
],
[
  verbose_output=0
])

# Strict Compile
AC_ARG_ENABLE(strict-compile,
              AS_HELP_STRING([--enable-strict-compile],
                             [Enable strict compilation (warnings are errors).]),
[
  if test "$enableval" != "no"; then
    strict_compile="-std=c99 -Wstrict-overflow=1 -Wextra -Wno-missing-field-initializers -Wshadow -Wpointer-arith -Wstrict-prototypes -Wmissing-prototypes -Wno-unused-parameter -Wformat -Wformat-security -Werror -fstack-protector -D_FORTIFY_SOURCE=2"
  else
    strict_compile=
  fi
],
[
  strict_compile=
])

# DEBUG_CONF
AC_ARG_ENABLE(debug-conf,
              AS_HELP_STRING([--enable-debug-conf],
                             [Enable debug during configuration.]),
[
  if test "$enableval" != "no"; then
    debug_conf="-DDEBUG_CONF"
  else
    debug_conf=
  fi
],
[
  debug_conf=
])

# CACHE_DEBUG
AC_ARG_ENABLE(debug-cache,
              AS_HELP_STRING([--enable-debug-cache],
                             [Enable debug for transformation caching.]),
[
  if test "$enableval" != "no"; then
    debug_cache="-DCACHE_DEBUG"
  else
    debug_cache=
  fi
],
[
  debug_cache=
])

# DEBUG_ACMP
AC_ARG_ENABLE(debug-acmp,
              AS_HELP_STRING([--enable-debug-acmp],
                             [Enable debugging acmp code.]),
[
  if test "$enableval" != "no"; then
    debug_acmp="-DDEBUG_ACMP"
  else
    debug_acmp=
  fi
],
[
  debug_acmp=
])

# DEBUG_MEM
AC_ARG_ENABLE(debug-mem,
              AS_HELP_STRING([--enable-debug-mem],
                             [Enable debug during configuration.]),
[
  if test "$enableval" != "no"; then
    debug_mem="-DDEBUG_MEM"
  else
    debug_mem=
  fi
],
[
  debug_mem=
])

# PERFORMANCE_MEASUREMENT
AC_ARG_ENABLE(performance-measurement,
              AS_HELP_STRING([--enable-performance-measurement],
                             [Enable performance-measurement stats.]),
[
  if test "$enableval" != "no"; then
    perf_meas="-DPERFORMANCE_MEASUREMENT"
  else
    perf_meas=
  fi
],
[
  perf_meas=
])

# NO_MODSEC_API
AC_ARG_ENABLE(modsec-api,
              AS_HELP_STRING([--disable-modsec-api],
                             [Disable the API; compiling against some older Apache versions require this.]),
[
  if test "$enableval" != "yes"; then
    modsec_api="-DNO_MODSEC_API"
  else
    modsec_api=
  fi
],
[
  modsec_api=
])

# Find apxs
AC_MSG_NOTICE(looking for Apache module support via DSO through APXS)
AC_ARG_WITH(apxs,
            [AS_HELP_STRING([[--with-apxs=FILE]],
                            [FILE is the path to apxs; defaults to "apxs".])],
[
  if test "$withval" = "yes"; then
    APXS=apxs
  else
    APXS="$withval"
  fi
])

if test -z "$APXS"; then
  for i in /usr/local/apache22/bin \
           /usr/local/apache2/bin \
           /usr/local/apache/bin \
           /usr/local/sbin \
           /usr/local/bin \
           /usr/sbin \
           /usr/bin;
  do
    if test -f "$i/apxs2"; then
      APXS="$i/apxs2"
      break
    elif test -f "$i/apxs"; then
      APXS="$i/apxs"
      break
    fi
  done
fi

# arbitrarily picking the same version subversion looks for, don't know how
# accurate this really is, but at least it'll force us to have apache2...
HTTPD_WANTED_MMN=20020903

if test -n "$APXS" -a "$APXS" != "no" -a -x "$APXS" ; then
  APXS_INCLUDE="`$APXS -q INCLUDEDIR`"
  if test -r $APXS_INCLUDE/httpd.h; then
    AC_MSG_NOTICE(found apxs at $APXS)
    AC_MSG_NOTICE(checking httpd version)
    AC_EGREP_CPP(VERSION_OK,
    [
#include "$APXS_INCLUDE/ap_mmn.h"
#if AP_MODULE_MAGIC_AT_LEAST($HTTPD_WANTED_MMN,0)
VERSION_OK
#endif],
    [AC_MSG_NOTICE(httpd is recent enough)],
    [
     if test "$report_errors" -eq 1; then
       AC_MSG_ERROR(apache is too old, mmn must be at least $HTTPD_WANTED_MMN)
     else
       AC_MSG_NOTICE(apache is too old, mmn must be at least $HTTPD_WANTED_MMN)
     fi
    ])
  fi
  APXS_INCLUDEDIR="`$APXS -q INCLUDEDIR`"
  if test "$verbose_output" -eq 1; then AC_MSG_NOTICE(apxs INCLUDEDIR: $APXS_INCLUDEDIR); fi
  # Make sure the include dir is used
  if test -n "$APXS_INCLUDEDIR"; then
    APXS_INCLUDES="-I${APXS_INCLUDEDIR} `$APXS -q INCLUDES` `$APXS -q EXTRA_INCLUDES`"
  else
    APXS_INCLUDES="`$APXS -q INCLUDES` `$APXS -q EXTRA_INCLUDES`"
  fi
  if test "$verbose_output" -eq 1; then AC_MSG_NOTICE(apxs INCLUDES: $APXS_INCLUDES); fi
  APXS_CFLAGS=-I`$APXS -q INCLUDEDIR`
  if test "$verbose_output" -eq 1; then AC_MSG_NOTICE(apxs CFLAGS: $APXS_CFLAGS); fi
  APXS_LDFLAGS=
  if test "$verbose_output" -eq 1; then AC_MSG_NOTICE(apxs LDFLAGS: $APXS_LDFLAGS); fi
  APXS_LIBDIR="`$APXS -q LIBDIR`"
  if test "$verbose_output" -eq 1; then AC_MSG_NOTICE(apxs LIBDIR: $APXS_LIBDIR); fi
  # Make sure the lib dir is used
  if test -n "$APXS_LIBDIR"; then
    APXS_LIBS="-L${APXS_LIBDIR} `$APXS -q LIBS` `$APXS -q EXTRA_LIBS`"
  else
    APXS_LIBS="`$APXS -q LIBS` `$APXS -q EXTRA_LIBS`"
  fi
  if test "$verbose_output" -eq 1; then AC_MSG_NOTICE(apxs LIBS: $APXS_LIBS); fi
  APXS_LIBTOOL="`$APXS -q LIBTOOL`"
  if test "$verbose_output" -eq 1; then AC_MSG_NOTICE(apxs LIBTOOL: $APXS_LIBTOOL); fi
  APXS_CC="`$APXS -q CC`"
  if test "$verbose_output" -eq 1; then AC_MSG_NOTICE(apxs CC: $APXS_CC); fi
  APXS_BINDIR="`$APXS -q BINDIR`"
  if test "$verbose_output" -eq 1; then AC_MSG_NOTICE(apxs BINDIR: $APXS_BINDIR); fi
  APXS_SBINDIR="`$APXS -q SBINDIR`"
  if test "$verbose_output" -eq 1; then AC_MSG_NOTICE(apxs SBINDIR: $APXS_SBINDIR); fi
  APXS_PROGNAME="`$APXS -q PROGNAME`"
  if test "$verbose_output" -eq 1; then AC_MSG_NOTICE(apxs PROGNAME: $APXS_PROGNAME); fi
  APXS_LIBEXECDIR="`$APXS -q LIBEXECDIR`"
  if test "$verbose_output" -eq 1; then AC_MSG_NOTICE(apxs LIBEXECDIR: $APXS_LIBEXECDIR); fi
  APXS_MODULES=$APXS_LIBEXECDIR
  if test "$verbose_output" -eq 1; then AC_MSG_NOTICE(apxs MODULES: $APXS_MODULES); fi
  if test "$APXS_SBINDIR" = "/"; then
    APXS_HTTPD="$APXS_SBINDIR/$APXS_PROGNAME"
  else
    APXS_HTTPD="$APXS_SBINDIR/$APXS_PROGNAME"
  fi
  if test "$verbose_output" -eq 1; then AC_MSG_NOTICE(apxs HTTPD: $APXS_HTTPD); fi
else
  if test "$report_errors" -eq 1; then
    AC_MSG_ERROR(couldn't find APXS)
  else
    AC_MSG_NOTICE(couldn't find APXS)
  fi
fi

# Include M4 macros
sinclude(build/find_pcre.m4)
sinclude(build/find_apr.m4)
sinclude(build/find_apu.m4)
sinclude(build/find_xml.m4)
sinclude(build/find_lua.m4)
sinclude(build/find_curl.m4)


### Build *EXTRA_CFLAGS vars

# Allow overriding EXTRA_CFLAGS
if $ENV_CMD | $GREP "^EXTRA_CFLAGS" > /dev/null 2>&1; then
  if test -z "$debug_mem"; then
    EXTRA_CFLAGS="$EXTRA_CFLAGS $strict_compile"
  fi
else
  if test -n "$debug_mem"; then
    EXTRA_CFLAGS="-O0 -g -Wall"
  else
    EXTRA_CFLAGS="-O2 -g -Wall $strict_compile"
  fi
fi
MODSEC_EXTRA_CFLAGS="$pcre_study $pcre_match_limit $pcre_match_limit_recursion $debug_conf $debug_cache $debug_acmp $debug_mem $perf_meas $modsec_api"

APXS_WRAPPER=build/apxs-wrapper
APXS_EXTRA_CFLAGS=""
for f in $EXTRA_CFLAGS; do
    APXS_EXTRA_CFLAGS="$APXS_EXTRA_CFLAGS -Wc,$f"
done;
MODSEC_APXS_EXTRA_CFLAGS=""
for f in $MODSEC_EXTRA_CFLAGS; do
    MODSEC_APXS_EXTRA_CFLAGS="$MODSEC_APXS_EXTRA_CFLAGS -Wc,$f"
done;

### Substitute the vars

AC_SUBST(TOPLEVEL_SUBDIRS)
AC_SUBST(EXTRA_CFLAGS)
AC_SUBST(MODSEC_EXTRA_CFLAGS)
AC_SUBST(APXS)
AC_SUBST(APXS_WRAPPER)
AC_SUBST(APXS_INCLUDEDIR)
AC_SUBST(APXS_INCLUDES)
AC_SUBST(APXS_EXTRA_CFLAGS)
AC_SUBST(MODSEC_APXS_EXTRA_CFLAGS)
AC_SUBST(APXS_LDFLAGS)
AC_SUBST(APXS_LIBS)
AC_SUBST(APXS_CFLAGS)
AC_SUBST(APXS_LIBTOOL)
AC_SUBST(APXS_CC)
AC_SUBST(APXS_LIBDIR)
AC_SUBST(APXS_BINDIR)
AC_SUBST(APXS_SBINDIR)
AC_SUBST(APXS_PROGNAME)
AC_SUBST(APXS_LIBEXECDIR)
AC_SUBST(APXS_MODULES)
AC_SUBST(APXS_HTTPD)

CHECK_PCRE()
if test "$build_apache2_module" -ne 0 -o "$build_mlogc" -ne 0; then
CHECK_APR()
CHECK_APU()
fi
CHECK_LIBXML2()
CHECK_LUA()
if test -n "$LUA_VERSION"; then
    LUA_CFLAGS="-DWITH_LUA $LUA_CFLAGS"
fi
if test "$build_mlogc" -ne 0; then
CHECK_CURL()
fi

AC_CONFIG_FILES([Makefile])
AC_CONFIG_FILES([tools/Makefile])
if test "$build_apache2_module" -ne 0; then
AC_CONFIG_FILES([apache2/Makefile])
fi
if test "$build_extentions" -ne 0; then
AC_CONFIG_FILES([ext/Makefile])
fi
AC_CONFIG_FILES([build/apxs-wrapper], [chmod +x build/apxs-wrapper])
if test -e "$PERL"; then
    if test "$build_mlogc" -ne 0; then
        AC_CONFIG_FILES([mlogc/mlogc-batch-load.pl], [chmod +x mlogc/mlogc-batch-load.pl])
    fi
    AC_CONFIG_FILES([tests/run-unit-tests.pl], [chmod +x tests/run-unit-tests.pl])
    AC_CONFIG_FILES([tests/run-regression-tests.pl], [chmod +x tests/run-regression-tests.pl])
    AC_CONFIG_FILES([tests/gen_rx-pm.pl], [chmod +x tests/gen_rx-pm.pl])
    AC_CONFIG_FILES([tests/csv_rx-pm.pl], [chmod +x tests/csv_rx-pm.pl])
    AC_CONFIG_FILES([tests/regression/server_root/conf/httpd.conf])

    # Perl based tools
    AC_CONFIG_FILES([tools/rules-updater.pl], [chmod +x tools/rules-updater.pl])
fi
if test "$build_mlogc" -ne 0; then
    AC_CONFIG_FILES([mlogc/Makefile])
fi
AC_CONFIG_FILES([tests/Makefile])

AC_OUTPUT