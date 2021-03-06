# KitchenSink App

The Kitchen sink Application will be a tool to test the functionality of the 
APIs across platforms as well as showcase the usage of the APIs. 

Tracking bug: https://bugzilla.mozilla.org/show_bug.cgi?id=830876 

# FxOS Installation

Easily install packaged and hosted apps using the Firefox OS remote debugging protocols.

## How it works

1. `Makefile`: *(Packaged app only)* Package all files from folder into `application.zip`
2. `Makefile`: Move important files to phone via `adb`
3. `Makefile`: Forward remote debugging port (6000) from device to computer (via `adb`)
4. `Makefile`: Run `install.js` via `xpcshell`
5. `install.js`: Remotely install app from folder using the [Webapp Actor](http://mxr.mozilla.org/mozilla-central/source/b2g/chrome/content/dbg-webapps-actors.js).

## Dependencies

Extract the following packages `~/bin`.

If you choose a different path, change the variables in `Makefile`):

	XPCSHELL = ~/bin/xulrunner-sdk/bin/xpcshell
	ADB = ~/bin/android-sdk/platform-tools/adb

### XULRunner (XPCShell)

http://ftp.mozilla.org/pub/mozilla.org/xulrunner/releases/18.0.2/runtimes/

### Android SDK (ADB)

http://developer.android.com/sdk/index.html#download

## Device Setup

Enable `Remote Debugging` in `Settings > Device Information > Developer`.

## Usage

### Packaged

See folder `my-package`. Your app should at least have an `index.html` and a `manifest.webapp` with the correct `launch_path`. App `type` can be either `web` or `privileged`.

Install packaged app from folder ``

	make FOLDER=my-package packaged install

### Hosted

See `my-hosted` folder. Your folder only needs to contain `manifest.webapp` and a `metadata.json`. In most cases you only need to adapt `origin` in `metadata.json` and `launch_path` in the manifest.

Install hosted app from folder `my-hosted`:

	make FOLDER=my-hosted hosted install

