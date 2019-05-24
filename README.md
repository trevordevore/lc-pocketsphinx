# lc-pocketsphinx

A LiveCode Builder wrapper around PocketSphinx. This project was created for the LiveCode Builder Foreign Function Interface Workshop at the LiveCode 2019 conference in San Jose, California. 

Basic usage tutorial:

https://cmusphinx.github.io/wiki/tutorialpocketsphinx/#basic-usage-hello-world

Github:

- https://github.com/cmusphinx/sphinxbase/
- https://github.com/cmusphinx/pocketsphinx/

## Testing

To test this project in LiveCode:

1. Open the Extension Builder from the Tools menu.
2. Load the pocketsphinx.lcb file and load it into the IDE. This article shows where the button is for testing an LCB file: http://lessons.livecode.com/m/4071/l/1035188-how-to-use-the-extension-builder
3. Open the pocketsphinx_test.livecode stack in the IDE.
4. Click the **Test** button. This will analyze the *goforward.raw* audio file included in the repo. You should hypothesis of the speech to text analysis appear in the log field.
5. If you have your own audio file to analyze click the **Select File...** button to select the file.

## Supported Audio Files

Audio files must be single-channel (monaural), little-endian, unheadered 16-bit signed PCM audio file sampled at 16000 Hz. You can record this files using Audacity:

https://www.audacityteam.org

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
