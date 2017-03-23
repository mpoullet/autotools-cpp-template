# Comment like in a normal Makefile

bin_PROGRAMS = hello

# All files should be added so that make dist take them in the tarball
# We do a non-recursive make so add the path to each file too
hello_SOURCES = src/main.cpp \
                src/main.hpp

# automake conditionals (conditional is set in configure.ac)
if DEBUG_ENABLED
hello_SOURCES += src/debug.cpp
endif

# By default, data files are NOT included in a distribution, so use the dist_/nodist_ modifier to change this on a per variable basis
dist_pkgdata_DATA = my_data.txt

# Flags that are needed for ALL targets in the Makefile:

# Flags for the C preprocessor
AM_CPPFLAGS = -include config.hpp
# Flags for the C++ compiler
AM_CXXFLAGS = -Wall -Wextra -Werror -pedantic
# Flags for the C compiler
AM_CFLAGS = -Wall -Wextra -Werror -pedantic

