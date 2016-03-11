profanity-plugins
=================

Plugin support for Profanity is currently in development.

* The `master` branch of Profanity now includes support for C and Python plugins.
* The `plugins` branch contains additional support for Ruby and Lua, but is unstable.

For a list of outstanding issues before releasing 0.5.0, see: https://github.com/boothj5/profanity/milestones/0.5.0

Building Profanity with plugin support
--------------------------------------

Additional dependencies required:

```
autoconf-archive
libtool
```

Plus the development packages for supported languages:

```
python-dev
lua-dev
ruby-dev
```

Build with the usual:

```
./bootstrap.sh
./configure
make
sudo make install
```

By default the build will look for required libraries and add plugin support if they are found.  After building, run `profanity -v` to see which language support is available, example output:

```
Profanity, version 0.5.0dev.plugins-python.63a7316
Copyright (C) 2012 - 2016 James Booth <boothj5web@gmail.com>.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>

This is free software; you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Build information:
XMPP library: libmesode
Desktop notification support: Enabled
OTR support: Enabled
PGP support: Enabled
C plugins: Enabled
Python plugins: Enabled
```

Installing plugins
------------------

1 - Copy the plugin

For Python, Ruby and Lua plugins, copy the plugin to `$XDG_DATA/profanity/plugins/`, (`~/.local/share/profanity/plugins/` on most systems).

For C plugins, build the plugin using the supplied Makefile, and then copy the `.so` file to the same location.

2 - Add to profrc

For all types of plugins, the list of plugins to acutally load when starting Profanity is defined in `$XDG_CONFIG/profanity/profrc` (`~/.config/profanity/profrc` on most systems).

For example:

```
[plugins]
load=browser.py;platform-info.py;ascii.py;pid.so
```

Getting help on plugins:

* `/plugins` - Shows a list of loaded plugins.
* `/help commands plugins` - Shows commands defined by plugins
* `/help <plugin_cmd>` - Show help for a plugin command, e.g. `/help browser`

Example plugin code
-------------------

Whilst the API is being developed, the following test plugins are a good reference of possible hooks and API calls available, (Ruby and Lua examples might not be up to date):

* [tests/test-c-plugin.c](https://github.com/boothj5/profanity-plugins/blob/master/tests/test-c-plugin/test-c-plugin.c)
* [tests/python-test.py](https://github.com/boothj5/profanity-plugins/blob/master/tests/python-test.py)
* [tests/RubyTest.rb](https://github.com/boothj5/profanity-plugins/blob/master/tests/RubyTest.rb)
* [tests/luatest.lua](https://github.com/boothj5/profanity-plugins/blob/master/tests/luatest.lua)


