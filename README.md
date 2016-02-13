pizmidi VST plugins
===================

This is a fork of piz midi, a comprehensive suite of VST MIDI plugins
available from <http://thepiz.org/pizmidi/>. These will be useful for anyone
working with MIDI in their musical projects, but note that they require a VST
host capable of loading pure MIDI plugins. (They should work fine with most
popular open-source and commercial Linux DAWs nowadays.)

As far as I can tell, the original sources are by Reuben Vinal from "Insert
Piz Here->", see <http://thepiz.org/plugins/?p=pizmidi>, and
<https://code.google.com/archive/p/pizmidi/> for the original source code. I
merely uploaded the repository to [Bitbucket][1] and did some minor touches to
fix the build system and make the plugins compile on Linux.

Documentation by the original author(s) is included in the `Release`
folder. In particular, check the `pizmidi.txt` file for the change log and the
`piz midi VST plugins.pdf` document (or the text files under `Release/doc`)
for the plugin descriptions.

Copying
-------

There's no licensing information on the pizmidi website and in the sources
AFAICT, but according to the archive of the original Google Code project the
source code is licensed under the GPLv2.

Installation
------------

Make sure that you have [Steinberg's VST SDK][2] installed in a location
searched by the Makefile (just unzipping Steinberg's package under any of the
directories listed in the `sdkpaths` make variable should do) and run
`make`. The compiled VSTs end up in the `Release` folder, from where you can
just copy or move them to your VST folder, along with the `pizmidi.ini` file.

A ready-made PKGBUILD for Arch Linux by yours truly is available from the
[Arch User Repositories][3] (AUR). Debian packages of pizmidi are provided by
falkTX, you can find these in the [KXStudio repositories][4]. Mac and Windows
binaries by the original author(s) can be found at
<http://thepiz.org/plugins/?p=pizmidi>.

[1]: https://bitbucket.org/agraef/pizmidi
[2]: http://www.steinberg.net/en/company/developers.html
[3]: https://aur.archlinux.org/packages/pizmidi-git/
[4]: http://kxstudio.linuxaudio.org/Repositories:Plugins

Enjoy. :)

Albert Graef <aggraef@gmail.com>, Feb 2016
