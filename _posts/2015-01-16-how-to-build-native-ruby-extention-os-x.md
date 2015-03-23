---
layout: post
title: "How to build native Ruby extention OS X"
published: false
description: ""
category: 
tags: [osx, ruby]
---


##Problem

```bash
# gem install nio4r
Building native extensions.  This could take a while...
ERROR:  Error installing nio4r:
ERROR: Failed to build gem native extension.
```

```bash
# gem install nio4r --verbose

Gem files will remain installed in /Users/kevit/.chefdk/gem/ruby/2.1.0/gems/nio4r-1.1.0 for inspection.
Results logged to /Users/kevit/.chefdk/gem/ruby/2.1.0/extensions/x86_64-darwin-12/2.1.0/nio4r-1.1.0/gem_make.out

```

```bash
# find /Users/kevit/.chefdk/gem -name mkmf.log |grep nio4r-1.1.0
/Users/kevit/.chefdk/gem/ruby/2.1.0/extensions/x86_64-darwin-12/2.1.0/nio4r-1.1.0/mkmf.log

# cat mkmf.log
"clang -o conftest -I/opt/chefdk/embedded/include/ruby-2.1.0/x86_64-darwin12.0 -I/opt/chefdk/embedded/include/ruby-2.1.0/ruby/backward -I/opt/chefdk/embedded/include/ruby-2.1.0 -I.  -I/opt/chefdk/embedded/include -D_XOPEN_SOURCE -D_DARWIN_C_SOURCE -D_DARWIN_UNLIMITED_SELECT -D_REENTRANT   -I/opt/chefdk/embedded/include -I/opt/chefdk/embedded/include/ncurses -arch x86_64 -O3 -g -pipe -Qunused-arguments -fno-common conftest.c  -L. -L/opt/chefdk/embedded/lib -L/opt/chefdk/embedded/lib -L. -L/opt/chefdk/embedded/lib -arch x86_64 -fstack-protector -L/opt/chefdk/embedded/lib   -m64   -lruby.2.1.0  -lpthread -ldl -lobjc "
dyld: Symbol not found: _iconv
Referenced from: /usr/lib/libcups.2.dylib
Expected in: /opt/chefdk/embedded/lib/libiconv.2.dylib
in /usr/lib/libcups.2.dylib
clang: error: unable to locate xcodebuild, please make sure the path to the Xcode folder is set correctly!
clang: error: You can set the path to the Xcode folder using /usr/bin/xcode-select -switch
```

##How to fix
* dowloading Command Line tools from  https://developer.apple.com/downloads/
* sudo xcode-select -switch /Library/Developer/CommandLineTools


##Another example with imagemagick/Rmagick
```
Can't install RMagick 2.13.4. Can't find MagickWand.h.
C_INCLUDE_PATH=/usr/local/Cellar/imagemagick/6.9.0-3/include/ImageMagick-6 PKG_CONFIG_PATH=/usr/local/Cellar/imagemagick/6.9.0-3/lib/pkgconfig gem install rmagick
```

##Links
* [imagemagick](http://stackoverflow.com/questions/9050419/cant-install-rmagick-2-13-1-cant-find-magickwand-h)
* [xcode](http://stackoverflow.com/questions/19647788/why-is-this-git-command-line-broken-after-a-fresh-os-x-mavericks-upgrade)
* [More about building native extensionr](http://patshaughnessy.net/2011/10/31/dont-be-terrified-of-building-native-extensions)
