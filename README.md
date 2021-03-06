# termcolors-mv

(C) Martin Väth <martin at mvath.de>
This project is under the MIT license
SPDX-License-Identifier: MIT

256colors sample script, dircolors configuration files, and a dircolors wrapper

For gentoo, the package is available over the mv overlay (via layman).

This package contains two scripts and some "dircolors" colorschemes,
all appropriate for unix type terminals with 8/16 and 256 colors.

To create the dircolor schemes create e.g. the directory `etc/dir_colors`
or `lib/dir_colors`, change into it, and call the `bin/DIR_COLORS-create`
script (perl is needed).
These colorschemes are appropriate for 8/16 colors or 256 colors, respectively,
and they were developed for standard system colors and
Ethan Schoonover's solarized colorscheme, respectively.

The system color schemes are developed for black background terminals, only.

The solarized versions work with both, light and dark versions of
the solarized colorscheme, and if you use them you are responsible on your
own to set the terminal colors so that the 8/16 system colors are mapped
to the colors from the solarized scheme.
The 256-color solarized scheme adds some more colors to the original scheme
to allow a richer distinction of files.

To use the color schemes you can call
-	```eval "`dircolors [path to desired color scheme]`"```

For a fixed installation, I recommend to copy `etc/dir_colors/*`
(or `lib/dir_colors/*`) to one of the directories
-	`$DEFAULTS/dir_colors/`
-	`$HOME/.dir_colors/`
-	`$HOME/.config/dir_colors/`
-	`/etc/dir_colors/`
-	`/usr/lib/dir_colors/`
-	`/lib/dir_colors/`

and to use the dircolors-mv wrapper mentioned below which will look for the
appropriate file in the above directories (in the mentioned order).

The scripts (in `bin`) are:

### 256colors

A small perl script which just displays 256 colors on capable
terminals in a systematic manner. The usage should be self-explaining.
Calling `256colors man` shows you some further options.

### dircolors-mv

This script is a wrapper for dircolors.
If you copy this script into your path you can use
-	```eval "`dircolors-mv`"```

if you followed the above suggestion about the location (see below).
This will pick the corresponding file depending on the environment variables
-	`TERM`
	(to determine whether the terminal is 8-bit capable by some heuristics)
-	SOLARIZED (to determine whether output for solarized is desired)
-	DEFAULTS (for the path mentioned above)

If the heuristics for the terminal does not work for you, just export `TERM`
locally, e.g.
-	```eval "`TERM=xterm-256colors dircolors-mv`"```

will force a 256 color scheme.
Concerning the location, the first readable non-directory for the match will
be used. This way, there can be e.g. distribution defaults in
`/usr/lib/dir_colors/` which can be overridden by the local administrator in
`/etc/dir_colors/` which in turn can be overridden by the user which in turn
can be overridden by the environment variable `$DEFAULT`.
To protect a file from being used you can e.g. symlink it to `/dev/null`
in a higher precedence directory.

### DIR_COLORS-create

This script will generate in the current directory:
-	`DIR_COLORS`
-	`DIRCOLORS-solarized`
-	`DIRCOLORS-256`
-	`DIRCOLORS-solarized-256`

(if these files exist they are overridden without any warning).
These files are the dircolor schemes for normal and solarized mode in
8/16 or 256 color terminals, respectively.
