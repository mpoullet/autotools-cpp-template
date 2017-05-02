# Comment like in a normal Makefile

bin_PROGRAMS = hello_cpp

# All files should be added so that make dist take them in the tarball
# We do a non-recursive make so add the path to each file too
hello_cpp_SOURCES = src/main.cpp \
                src/main.hpp

# automake conditionals (conditional is set in configure.ac)
if DEBUG_ENABLED
hello_cpp_SOURCES += src/debug.cpp
endif

# By default, data files are NOT included in a distribution, so use the dist_/nodist_ modifier to change this on a per variable basis
dist_pkgdata_DATA = my_data.txt

# Flags needed for ALL targets in the Makefile
# C preprocessor
AM_CPPFLAGS = -include config.hpp
# C++ compiler
AM_CXXFLAGS = -Wall -Wextra -Werror -pedantic
# C compiler
AM_CFLAGS = -Wall -Wextra -Werror -pedantic

include $(top_srcdir)/other_tool/Makefile.am
