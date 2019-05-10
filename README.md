# lc-pocketsphinx
LiveCode Builder wrapper around PocketSphinx

Basic usage tutorial:

https://cmusphinx.github.io/wiki/tutorialpocketsphinx/#basic-usage-hello-world

Github:

- https://github.com/cmusphinx/sphinxbase/
- https://github.com/cmusphinx/pocketsphinx/

## Troubleshooting tip

`-logfn` command line param specifies path to log file. Set in order to get detailed output about what is going on.

## Building on macOS

Follow instructions on github site but specify your own install folder where `make install` will place dylibs you need:

```
./configure --prefix=/Users/trevordevore/Downloads/pocketsphinx/install
```

After building the sphinxbase and pocketsphinx dylibs on macOS the search paths for the shared libaries needed to be updated. 

- Copy libsphinxbase.3.dylib and libpocketsphinx.3.dylib to the `./code/x86_64-mac` folder.
- Remove `lib` and `.3` from the file names so that they match the DLL names.
- Update search paths. 

sphinxbase.dylib was modified as follows: 

```
install_name_tool -id "@loader_path/sphinxbase.dylib" sphinxbase.dylib
```

pocketsphinx.dylib was modified as follows:

```
install_name_tool -id "@loader_path/pocketsphinx.dylib" pocketsphinx.dylib

install_name_tool -change "/usr/local/lib/libsphinxbase.3.dylib" "@loader_path/sphinxbase.dylib" pocketsphinx.dylib
```
