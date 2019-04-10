# Locate Visual Studio installations in Python and C

Locating Visual Studio installations can be suprisingly hard. This repostitory provides basic implementations for doing this in Python and C, by using the Visual Studio Setup Configuration utility DLL installed by Visual Studio. The code is released to the public domain.

## Python

Use the provided function to get a list of version and path tuples of all installed versions of Visual Studio

```
from vslocate import get_vs_installations

for version, path in get_vs_installations():
	print(version + " " + path)
```

or run the script directly

```
python vslocate.py
```

The output is one line per installation with version number and path, for example

```
15.9.28307.586 C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise
16.0.28729.10 C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise
```

## C

Use the enumeration function to get a callback for each installed version of Visual Studio

```
#include <stdio.h>

void
my_callback(const wchar_t* version, const wchar_t* path) {
	printf("%ls %ls\n", version, path);
}

int
main(int argc, char** argv) {
	(void)sizeof(argc);
	(void)sizeof(argv);

	return get_vs_installations(my_callback);
}
```

Or, to compile the C tool use

```
cl /O1 /Os /Gm- /GF- /sdl /MT /GS /D COMPILE_TOOL=1 vslocate.c /link /out:vslocate.exe
```

or

```
clang -Oz -DCOMPILE_TOOL=1 vslocate.c -o vslocate.exe
```

The output of the tool is one line per installation with version number and path, for example

```
15.9.28307.586 C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise
16.0.28729.10 C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise
```
