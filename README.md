# Locate Visual Studio installations in Python and C (public domain)

Locating Visual Studio installations can be suprisingly hard. This repostitory provides basic implementations for doing this in Python and C, by using the Visual Studio Setup Configuration utility DLL installed by Visual Studio.

## Python

```
from vslocate import get_installations

for version, path in get_installations():
	print(version + " " + path)
```

or

```
python vslocate.py
```

The output is one line per installation with version number and path, for example

```
15.9.28307.586 C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise
16.0.28729.10 C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise
```

## C

To compile the C tool use

```
cl /O1 /Os /Gm- /GF- /sdl /MT /GS vslocate.c /link /out:vslocate.exe
```

or

```
clang -Oz vslocate.c -o vslocate.exe
```

The output is one line per installation with version number and path, for example

```
15.9.28307.586 C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise
16.0.28729.10 C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise
```
