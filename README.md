# snap-basics
Introduction to Snap packages for Ubuntu

## Autotools Setup
1. Go to the proj directory 'snap-basic'
2. Create the following directories

```bash
# move to project root
mkdir code
cd code
mkdir src
mkdir test
mkdir build
mkdir m4
```

3. Write your main source code
```bash
cd src
nano main.c # Write your code here
```

src/main.c
```c
#include <stdio.h>
int main(int argc, char *argv[]) {
    puts("Hello World");
    return 0;
}
```

4. Create your Automake file

```bash
cd ..
nano Makefile.am
```

Makefile.am
```Makefile
# subdir-objects flag added to enable backwards compatibility. Will be enabled by default in the future.
AUTOMAKE_OPTIONS = subdir-objects
bin_PROGRAMS = snap_basic

snap_basic_SOURCES = \
	src/main.c
```

5. Create your configure.ac file
```bash
sudo apt-get install autoconf
autoscan
rm autoscan.log
rm configure.scan 
nano configure.ac
```

configure.ac

```Makefile
AC_PREREQ([2.69])
# change your package name, version and bug-report-address here
AC_INIT([snap_basic], [0.0.1], [])
AC_CONFIG_SRCDIR([src/main.c])
AC_CONFIG_HEADERS([config.h])
# add the next line to use autoconf with automake
# -Wall   -> enable all warnings
# -Werror -> set all warnings as errors
# foreign -> treat it as foreign project
AM_INIT_AUTOMAKE([-Wall -Werror foreign])

# Checks for programs.
AC_PROG_CC

# Checks for libraries.

# Checks for header files.

# Checks for typedefs, structures, and compiler characteristics.

# Checks for library functions.

AC_CONFIG_FILES([Makefile])
AC_OUTPUT
```

6. Reconfigure the autoconf system after you made changes to your configuration file
```bash
autoreconf -vi
# -i -> copy missing auxillary files
```

7. Test your project
```bash
cd build
../configure
sudo apt-get install make
make
./snap_basic
# if it shows "Hello World", then you did everything successfully.
```

8. Rebuilding after making any changes to src/main.c
```
cd src
# make changes to main.c
cd ../build
make
./snap_basic
```

#### References
1. https://www.youtube.com/watch?v=dc1kEJvS248