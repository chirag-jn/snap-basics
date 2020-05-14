# snap-basics
Introduction to Snap packages for Ubuntu

## Autotools Setup
1. Go to the proj directory 'snap-basic'
2. Create the following directories

```bash
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

```c
// src/main.c
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

```am
AUTOMAKE_OPTIONS = subdir-objects
bin_PROGRAMS = snap_basic

snap_basic_SOURCES = \
	src/main.c
```

#### References
1. https://www.youtube.com/watch?v=dc1kEJvS248