# TIDAL for Linux

## What is this?

This is a wrapper for TIDAL's web app, using Nativfier, which injects custom code to provide for a better desktop experience. It adds the following features to TIDAL:

- Close to tray
- Desktop Notifications
- Global keyboard shortcuts (by default, bound to media keys)

## Installation

### From binary

Go to the releases tab, and download the latest `tar.xz` file. Extract it, run `chmod +x tidal`, and then you can run `tidal`.

### From source

#### Requirements

- Node
- NPM

#### Procedure

> This has been tested on Ubuntu 18.04.2 LTS - general steps will be the same, however the path of libpepflashplayer may change

1. Open up Chrome, and head to `chrome://components`. Click "Check for update" under Adobe Flash Player
2. Clone / download this repository
3. Open up a terminal in said directory
4. Change directory to this project, and type `npm install`
5. Run `npm run build`
6. Change directory to `build/tidal-linux-x64` and run `./tidal` - note, your working directory *has* to contain libpepflashplayer, so if you're making custom launchers, ensure this is set up right

### FAQ

#### Why Electron!? Electron is garbage! I want a native app!

To be honest, same, but, I don't have the time (this entire thing took about an hour or two to get working). This method of injecting code is far easier to get working, and, at the end of the day, works.

#### Can I disable notifications?

Not through an option in the interface, no. However, you can open up `resources/app/inject/inject.js`, and change the option `enable_notifications` to `False`. If you want this to be persitant across builds, change this in `custom.js`.

#### How do I change the shortcuts from media keys?

If you want to change the keyboard shortcuts, open up `resources/app/nativefier.json`, and scroll down to `"globalShortcuts"`, and modify it as needed. Make sure you only change `"key"` not `"inputEvents"`, or your keys will fail to register inside TIDAL. Once you've done this, run `npm run build`, and the new binary will use your new keybinds.

#### What's libpepflashplayer.so?

TIDAL either wants to use HTML5 powered DRM, or if that's not avaliable, it does it in Flash. Therefore, we include `libpepflashplayer.so` (the flash player binary provided by Google Chrome). By including it, the workaround of using Flash seems to work, and if you remove it, you get a message from TIDAL asking you to install Flash, or install their desktop app (a sick joke tbh). The only condition of this is that it means libpepflashplayer.so needs to be in the working directory when launching TIDAL (so, no `build/tidal-linux-x64`, it's `cd build/tidal-linux-x64 && ./tidal`). 

#### Why am I still getting the *no Flash* popup?

Make sure you have `libpepflashplayer.so` in the directory you're running `npm run build` in. If that still doesn't work, open up main.js, and change the location of `libpepflashplayer.so` to exactly where it is stored on your system.

#### Are you sure there isn't a better way than this mess?

There *kind of* is (if you're okay with more Electron that is). Plex added support for TIDAL, all proper like, and their desktop apps also support it (however seem to be Electron powered, or at least, Plexamp is). If you link a Plex account to your TIDAL account, you don't actually need a Plex server to use TIDAL (last time I checked anyway). This is here for those who don't want to use Plex, or want easy access to the features Plex doesn't have *just* yet, like Mixes or Discovery features.