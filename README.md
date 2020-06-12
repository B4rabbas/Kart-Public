Forked to change the bind/event key recognition (in https://github.com/B4rabbas/Kart-Public/blob/master/src/sdl/i_video.c https://github.com/B4rabbas/Sonic-Kart/edit/master/README.md)

# SRB2Kart

[SRB2Kart](https://srb2.org/mods/) is a kart racing mod based on the 3D Sonic the Hedgehog fangame [Sonic Robo Blast 2](https://srb2.org/), based on a modified version of [Doom Legacy](http://doomlegacy.sourceforge.net/).


## Dependencies
- NASM (x86 builds only)
- SDL2 (Linux/OS X only)
- SDL2-Mixer (Linux/OS X only)
- libupnp (Linux/OS X only)
- libgme (Linux/OS X only)

## Compiling on Ubuntu x64

Installing the dependencies :
```
sudo apt install -y libgme-dev libsdl2-mixer-dev libsdl2-dev zlib1g-dev libpng-dev nasm build-essential git libcurl4 libcurl4-openssl-dev
```

cloning source code :
```
git clone https://github.com/STJr/Kart-Public.git
```

Locate code source path : 
```
cd Kart-Public
```

Compiling : 
```
export LIBGME_CFLAGS=
export LIBGME_LDFLAGS=-lgme
make -C src/ LINUX64=1
```

Your executable is in 
```
~/Kart-Public/bin/Linux64
```

The game's assets are here : https://github.com/B4rabbas/Kart-Public/releases/tag/1.2

## One Line Compiling for Ubuntu x64

```
sudo apt install -y libgme-dev libsdl2-mixer-dev libsdl2-dev zlib1g-dev libpng-dev nasm build-essential git libcurl4 libcurl4-openssl-dev ; git clone https://github.com/STJr/Kart-Public.git ; cd Kart-Public ; export LIBGME_CFLAGS= ; export LIBGME_LDFLAGS=-lgme ; make -C src/ LINUX64=1
```

## Change the event system

```
Before start the compilation, open "src/sdl/i_video.c" in your favorite text editor

There is few replacements to do

Replace
(SDL_Scancode code)
by
(SDL_Keycode code)


code >= SDL_SCANCODE_
by
code >= SDLK_


code <= SDL_SCANCODE_
by
code <= SDLK_


code - SDL_SCANCODE_
by
code - SDLK_


code == SDL_
by
code == SDLK_


event.data1 = Impl_SDL_Scancode_To_Keycode(evt.keysym.scancode);
by
event.data1 = Impl_SDL_Scancode_To_Keycode(evt.keysym.sym);


case SDL_SCANCODE_
by
case SDLK_


Then add

#ifdef HWRENDER
	DBG_Printf("Unknown incoming scancode: %d, represented %c\n",
				code,
				SDL_GetKeyName(SDL_GetKeyFromScancode(code)));
#endif
	return 0;
}


before
static void SDLdoGrabMouse(void)
```

## Disclaimer
Kart Krew is in no way affiliated with SEGA or Sonic Team. We do not claim ownership of any of SEGA's intellectual property used in SRB2.
