AC_INIT([sbsigntool], [0.1], [jeremy.kerr@canonical.com])

AM_INIT_AUTOMAKE()

AC_PREREQ(2.60)

AC_CONFIG_HEADERS(config.h)
AC_CONFIG_SRCDIR(sbsign.c)

AC_PROG_CC
AM_PROG_CC_C_O
AC_PROG_CPP
AC_PROG_RANLIB

if test $cross_compiling = no; then
  AM_MISSING_PROG(HELP2MAN, help2man)
else
  HELP2MAN=:
fi

AC_MSG_CHECKING([build system endianness])
AC_PREPROC_IFELSE(
  [AC_LANG_PROGRAM([[#include <endian.h>]],
		   [[#if __BYTE_ORDER != __LITTLE_ENDIAN]]
		   [[#error]]
		   [[#endif]])],
  endian=little
  little_endian=1
  big_endian=0)

AC_PREPROC_IFELSE(
  [AC_LANG_PROGRAM([[#include <endian.h>]],
		   [[#if __BYTE_ORDER != __BIG_ENDIAN]]
		   [[#error]]
		   [[#endif]])],
  endian=big
  little_endian=0
  big_endian=1)


if test x"$endian" != "xbig" -a x"$endian" != "xlittle"; then
  AC_MSG_ERROR([Can't determine endianness; is endian.h present?])
fi
AC_MSG_RESULT($endian)
AC_DEFINE_UNQUOTED(HAVE_LITTLE_ENDIAN, $little_endian, [Little-endian system])
AC_DEFINE_UNQUOTED(HAVE_BIG_ENDIAN, $big_endian, [Big-endian system])

PKG_PROG_PKG_CONFIG()
PKG_CHECK_MODULES(libcrypto, libcrypto,
    [],
    AC_MSG_ERROR([libcrypto (from the OpenSSL package) is required]))

AC_CONFIG_FILES([Makefile lib/ccan/Makefile])
AC_OUTPUT