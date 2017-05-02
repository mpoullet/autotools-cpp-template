dnl autoscan && autoreconf -i && ./configure --disable-debug && cat my_config_file && make DESTDIR=/tmp/hello clean all install V=1
dnl find /tmp/hello && /tmp/hello/usr/local/bin/hello
dnl make dist && tar tf hello-1.0.tar.bz2 | sort
dnl git clean -xdf

dnl (Discard to Next Line) indicates a comment line
dnl sudo apt-get install autoconf automake libtool shtool autogen
dnl sudo apt-get install autoconf-archive
dnl GNU Autoconf Archive files are located in /usr/share/aclocal (Ubuntu)

dnl First, check if a recent version of autoconf is available
AC_PREREQ([2.69])

dnl Initialize Autoconf
AC_INIT([hello_cpp], [1.0], [http://hello.org/])
AC_MSG_NOTICE([Welcome to the AC_PACKAGE_NAME autoconf script.])
dnl Auxiliary directory: must be placed before the calls to AM_INIT_AUTOMAKE and LT_INIT
AC_CONFIG_AUX_DIR([build-aux])

dnl Initialize Automake
dnl Automake will generate Makefile.in at "autoreconf -i" time
dnl so we need to add Makefile (without the .in extension) to AC_CONFIG_FILES
dnl foreign tells automake to not require all the GNU Coding Style such as NEWS, README, AUTHORS
dnl subdir-objects allows a Makefile ot reference code in another directory => needed for non-recursive make
AM_INIT_AUTOMAKE([foreign dist-bzip2 subdir-objects 1.14])
dnl configure will generate the final Makefile from Makefile.in
AC_CONFIG_FILES([Makefile])
dnl Silent rules: the output is quiet by default and verbose if V=1 is passed
AM_SILENT_RULES([yes])

dnl Check for C++
AC_PROG_CXX
dnl AX_CXX_COMPILE_STDCXX_11 can be used with or without arguments
dnl [noext] indicates strict conformance mode (-std=c++11)
dnl [mandatory] indicates that the macro should error if no mode with that support is found
AX_CXX_COMPILE_STDCXX_11([noext], [mandatory])
AX_CXX_HAVE_STL

dnl Check for Boost and set BOOST_CPPFLAGS and BOOST_LDFLAGS
dnl Check Boost version manually: dpkg -S /usr/include/boost/version.hpp
AX_BOOST_BASE([1.58],, [AC_MSG_ERROR([AC_PACKAGE_NAME needs Boost, but it was not found in your system])])

dnl Configuration header
dnl Sanity test: check if the input template file exists in the current source tree
AC_CONFIG_SRCDIR([config.hpp.in])
dnl Autoheader will generate config.h.in at "autoreconf -i" time
dnl -DHAVE_CONFIG_H automatically added to CXX command line
AC_CONFIG_HEADERS([config.hpp])
dnl configure will generate the final config.h from config.h.in
dnl AC_DEFINE is for configuration headers NOT configuration files
AC_DEFINE([MY_DEFINE_VALUE], [11], [This is the MY_DEFINE_VALUE value])

dnl Check for functions
dnl Override test result with ./configure ac_cv_func_foobar=yes
AC_CHECK_FUNCS([printf foobar])

dnl Check for a library containing dlopen, e.g. in libdl
dnl Note: it's probably better to use pkg-config for this
AC_SEARCH_LIBS([dlopen], [dl])

dnl Using external software --with(out)-<package>=<arg>
AC_ARG_WITH([some_external_package],
    [AS_HELP_STRING([--with-some_external_package], [Use some_external_package])],
    [echo "Value given: ${withval}"],
    [echo "Value not given"])
echo "with_some_external_package = ${with_some_external_package}"

dnl Using package options --(en|dis)able-<feature>
dnl Demonstrating the use of a default value
AC_ARG_ENABLE([debug],
    [AS_HELP_STRING([--enable-debug], [Enable debug])],
    [echo "Value given: ${enableval}"],
    [enable_debug=yes])
echo "enable_debug = ${enable_debug}"

dnl The recommended way to run test is test "x$variable" = "x$value" to avoid null cases of the shell variable
AS_IF([test "x${enable_debug}" = "xyes"], [AC_DEFINE([DEBUG_ENABLED], [1], [Whether debugging is enabled])],
      [test "x${enable_debug}" = "xno"] , [AC_DEFINE([DEBUG_ENABLED], [0], [Whether debugging is enabled])])

dnl pkg-config
dnl *.pc files are part of the development files for the library
PKG_CHECK_MODULES([CURL], [libcurl])

dnl Process some config file
AC_CONFIG_FILES([my_config_file])
dnl AC_SUBST is for configuration files NOT configuration headers
AC_SUBST([MY_VAR], [11])

dnl Echo some infos (see AS_* macros to write shell script constructs)
AS_ECHO(["The value of CXX is ${CXX}"])

dnl automake conditionals
AM_CONDITIONAL([DEBUG_ENABLED], [test "x${enable_debug}" = "xyes"])

AC_OUTPUT
