# sm64ex-web

Modifications to original project Dockerfile to build the emscripten web version of sm64ex

You can probably do this on bare metal by installing emsdk version 1.39.5 along with all normal sm64ex dependencies, but easier to use docker

Instructions:

```
git clone https://github.com/queenkjuul/sm64ex-web.git
cd sm64ex-web
cp /path/to/your/baserom.us.z64 .
docker build . -t sm64ex --target web
docker run --rm -v $(pwd):/sm64ex sm64ex make TARGET_WEB=1 -j$(nproc)
docker run --rm -v $(pwd):/sm64ex sm64ex make TARGET_WEB=1 -j$(nproc)
```

Yes, that one command is run twice. No idea why that is necessary, but it is.

After successful build, you can easily test if you have Node installed:

```
cd build/us_web
npx http-server
```

## Additional features

I can't get fullscreen working, or real time canvas resizing, but I did add build flags that let you specify the width and height:

```
docker run --rm -v $(pwd):/sm64ex sm64ex make TARGET_WEB=1 WINDOW_WIDTH=1280 WINDOW_HEIGHT=720 -j$(nproc)
```

# sm64ex
Fork of [sm64-port/sm64-port](https://github.com/sm64-port/sm64-port) with additional features. 

Feel free to report bugs and contribute, but remember, there must be **no upload of any copyrighted asset**. 
Run `./extract_assets.py --clean && make clean` or `make distclean` to remove ROM-originated content.

Please contribute **first** to the [nightly branch](https://github.com/sm64pc/sm64ex/tree/nightly/). New functionality will be merged to master once they're considered to be well-tested.

## New features

 * Options menu with various settings, including button remapping.
 * Optional external data loading (so far only textures and assembled soundbanks), providing support for custom texture packs.
 * Optional analog camera and mouse look (using [Puppycam](https://github.com/FazanaJ/puppycam)).
 * Optional OpenGL1.3-based renderer for older machines, as well as the original GL2.1, D3D11 and D3D12 renderers from Emill's [n64-fast3d-engine](https://github.com/Emill/n64-fast3d-engine/).
 * Option to disable drawing distances.
 * Optional model and texture fixes (e.g. the smoke texture).
 * Skip introductory Peach & Lakitu cutscenes with the `--skip-intro` CLI option
 * Cheats menu in Options (activate with `--cheats` or by pressing L thrice in the pause menu).
 * Support for both little-endian and big-endian save files (meaning you can use save files from both sm64-port and most emulators), as well as an optional text-based save format.

For example `--savepath .` will read saves from the current directory (which not always matches the exe directory, but most of the time it does);
   `--savepath '!'` will read saves from the executable directory.

## Building
For building instructions, please refer to the [wiki](https://github.com/sm64pc/sm64ex/wiki).

**Make sure you have MXE first before attempting to compile for Windows on Linux and WSL. Follow the guide on the wiki.**
