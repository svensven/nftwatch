
nftwatch
========

![](nftwatch.png)

Copyright (C) 2021+ Kenneth Aaron.

flyingrhino AT orcon DOT net DOT nz

Freedom makes a better world: released under GNU GPLv3.

https://www.gnu.org/licenses/gpl-3.0.en.html

This software can be used by anyone at no cost, however,
if you like using my software and can support - please
donate money to a children's hospital of your choice.

This program is free software: you can redistribute it
and/or modify it under the terms of the GNU General Public
License as published by the Free Software Foundation:
GNU GPLv3. You must include this entire text with your
distribution.

This program is distributed in the hope that it will be
useful, but WITHOUT ANY WARRANTY; without even the implied
warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR
PURPOSE.
See the GNU General Public License for more details.


About nftwatch
--------------

* Shows nftables policy in a more readable format.
* Live counters table (if you enabled counters in nft).
* Scrollable output.
* User-configurable refresh speed.
* Pause display refresh.


Manual install instructions
---------------------------

* Clone/download the project from the git repository.
* Required: Copy to:  `/usr/local/bin/nftwatch`  and: +x it.
* Optional: Copy to:  `/etc/nftwatch.yml`
* `nftwatch`  with no args to run it.
* `nftwatch -m`  for this man page.


Configuring nftwatch
--------------------

Some configs are in:  `nftwatch.yml`    .
Others are hardcoded into the code - subject to improvement.
Config file will be loaded from these paths - whichever
is found first. If no config file is found - builtin
defaults will be used.
It is safe to run nftwatch without a config file.

* ~/.config/nftwatch/nftwatch.yml
* ~/.nftwatch.yml
* ~/nftwatch.yml
* /etc/nftwatch.yml


Controls
--------

nftwatch is designed for interactive use. Simply run it
and it will start displaying your nftables stats.

The following keyboard controls are available:

- f:                Speed up the display refresh
- s:                Slow down the display refresh
- p:                Pause the display refresh
- .:                Toggles comment dot padding
- ,:                Toggles even more dot padding
- 0:                Toggles hiding rules with 0 packets counted
- Up arrow or N:    Scroll the table up
- Down arrow or n:  Scroll the table down
- Home or g:        Jump to table top
- End or G:         Jump to table bottom
- PgUp or b:        Page up in the table
- PgDn or space:    Page down in the table
- [                 Half page up in the table
- ]                 Half page down in the table
- Ctrl-q or q:      Quit


Man page
--------

* `nftwatch -m`  for this man page.


Usage tips
----------

* If you see something interesting - pause the display
and scroll the table if needed.

* Add counters to your nftables rules if you want to see
these values in nftwatch (by default nft rules don't have
counters).

* Slow down your display refresh rate to get more accurate
results, as well as pickup rules that are rarely hit.
Refresh rates of 1 second and above yield accurate stats.

* If short comments make it difficult to follow the line -
toggle dot padding with:  `.`  to improve readability.
This change will apply at next table redraw.
And if this isn't enough:  `,`  will give you even more
padding.

* To control the output of nftables - for example to omit
the contents of sets - use the config file:
`nftwatch.yml`  and edit the value of:
`nftwatch_config_NftCommandLine` .
`nft --help`  -->  `Options (ruleset list formatting)`
gives the various controls over nftables output - some
work with nftwatch (such as:  `--terse`)  and some dont.


Troubleshooting
---------------

Increase the logging verbosity with:  `nftwatch -d`
or permanently increase it in the code by changing this
line:  `LogLevel = logging.DEBUG`    .
Check  `journalctl -f`  for nftwatch logs.
There is even more logging available in the code: many
`LogWrite` lines are commented out due to too much
logging - enable them as required.

On rare occasions nftwatch exits and leaves the terminal
messed up. Fix this by typing:  `reset`  in the terminal.
I tried to fix this at the end of function:  main
but I still see it happen 5% of the time when running fast
refresh rates.
If anyone knows a solution please tell me.


Limitations
-----------

- This is the first release of nftwatch.
- There could be bugs.
- It can be improved.
- Features can be added.
- nftwatch is tied to the nft output. Any changes in nft
output will break nftwatch.
- Supports up to 9999 lines/nft-handles before display may
get messed up. Should be enough for most use cases though.
- The first cycle after changing refresh speed will be
incorrect; the second cycle onwards will be fine until
you change refresh speed again.
- nftwatch is not a performance measurement tool - there
are a few factors that prevent the BPS and PPS rates from
being accurate, but it serves its main purpose of being a
rules troubleshooting assistant as well as giving you
fairly accurate stats.
- Empty lines in the output come from nftables, not
nftwatch. nftables does not add an empty line before new
tables, therefore subsequent tables are printed directly
below the closing brace of the last block. For example -
can be seen in the table fail2ban adds.

I initially wrote nftwatch because I wanted a realtime
running output from nftables that was better than simply
looping it through:  `watch`. As of now - nftwatch serves
its purpose. Let's see what feature requests I receive and
if nftwatch can be improved for more use cases.


