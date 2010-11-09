!SLIDE
<a href="http://github.com/mattscilipoti/showoff_brew_your_own">
  <img style="position: absolute; top: 0; right: 0; border: 0;" src="http://s3.amazonaws.com/github/ribbons/forkme_right_darkblue_121621.png" alt="Fork me on GitHub">
</a>
# Brew Your Own
## An Experience Report

##@mattscilipoti

!SLIDE
# __mxcl__.github.com/__homebrew__/
## The missing package manager for OS X.

!SLIDE
# __wiki__
# Formula-Cookbook

!SLIDE bullets
# __steps__
----
* search
* create
* edit (meta, build, dependencies)
* test
* pull request

!SLIDE
# __example__
---
# _dialog_

!SLIDE
# __motivation__
---
# _cucumber-farmer_

!SLIDE bullets
# __search__
----
* issue tracker on github
* `$ brew search dialog`

!SLIDE
# Formula we don’t accept

!SLIDE bullets
# __steps__
----
* <del>_search_</del>
* **create**
* edit (meta, build, dependencies)
* test
* pull request

!SLIDE
# __create__
----
    $ brew create <url to tarball>

!SLIDE
## hint
----
# wikipedia

!SLIDE commandline
# __create__
----
    $ brew create ftp://invisible-island.net/dialog/dialog.tar.gz

!SLIDE
# __create__
----

    $ brew create ftp://invisible-island.net/dialog/dialog.tar.gz
    Formula name [dialog]: 

!SLIDE small
# __create__
----

    $ brew create ftp://invisible-island.net/dialog/dialog.tar.gz
    Formula name [dialog]:
    Warning: Version cannot be determined from URL.
    You'll need to add an explicit 'version' to the formula.

!SLIDE
    @@@ Ruby
    require 'formula'

    class Dialog <Formula
      url 'ftp://invisible-island.net/dialog/dialog.tar.gz'
      homepage ''
      md5 ''
    
      # depends_on 'cmake'
    
      def install
        system "./configure", "--disable-debug", "--disable-dependency-tracking",
                              "--prefix=#{prefix}"
        # system "cmake . #{std_cmake_parameters}"
        system "make install"
      end
    end

!SLIDE bullets
# __steps__
----
* <del>_search_</del>
* <del>_create_</del>
* **edit** (meta, build, dependencies)
* test
* pull request

!SLIDE
# __meta__
----
    @@@ Ruby
    require 'formula'
    
    class Dialog <Formula
      url 'ftp://invisible-island.net/dialog/dialog.tar.gz'
      homepage 'http://invisible-island.net/dialog/'
      md5 '519c0a0cbac28ddb992111ec2c3f82aa'
      version '1.1.20070704'
 
!SLIDE bullets
# MD5
----
* Read it (preferred)
* Calculate it: `$ md5 /path/to/tarball`
* Install it: `$ brew install -i foo`

!SLIDE
# __build__

!SLIDE
# __build__
----
    @@@ Ruby
      def install
        system "./configure", "--disable-debug", "--disable-dependency-tracking",
                              "--prefix=#{prefix}"
        # system "cmake . #{std_cmake_parameters}"
        system "make install"
      end

!SLIDE bullets
# __build__
----
#README
* cmake
* autotools

!SLIDE
# Library/Formula/

!SLIDE
# I couldn't find anything helpful

!SLIDE
# Prayed to the gods of 
# __default__

!SLIDE
# __You__ 
# should read
# the wiki

!SLIDE
# __seriously__

!SLIDE
# I installed it.

!SLIDE
# that was
<br/>
#__easy__

!SLIDE
# I <span class='webding'> </span> smart defaults

!SLIDE
# __build__
----
    @@@ Ruby
      def install
        system "./configure", "--disable-debug", "--disable-dependency-tracking",
                              "--prefix=#{prefix}"
        # system "cmake . #{std_cmake_parameters}"
        system "make install"
      end

!SLIDE
# __build__
----
    @@@ Ruby
      def install
        system "./configure", "--disable-debug", "--disable-dependency-tracking",
                              "--prefix=#{prefix}"
        system "make install"
      end

!SLIDE bullets
# __steps__
----
* <del>_search_</del>
* <del>_create_</del>
* **edit** (meta, _[build]_, _[dependencies]_)
* test
* pull request

!SLIDE
# __ depends_on__

!SLIDE
# `# depends_on 'cmake'`

!SLIDE
## `otool -L /usr/local/bin/dialog`

!SLIDE
## `otool -L /usr/local/`__bin__`/dialog`

!SLIDE
#    $ brew install -i foo
#    $ brew install -vd foo

!SLIDE
    @@@ Bash
    $ otool -L /usr/local/bin/dialog
    /usr/local/bin/dialog:
    	/usr/lib/libncurses.5.4.dylib (compatibility version 5.4.0, current version 5.4.0)
    	/usr/lib/libiconv.2.dylib (compatibility version 7.0.0, current version 7.0.0)
    	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 125.2.0)

!SLIDE bullets
# Library/Formula/

*	libncurses
*	libiconv
*	libSystem

!SLIDE
    @@@ Ruby
    depends_on 'libiconv'

!SLIDE
    @@@ Ruby
    require 'formula'

    class Dialog <Formula
      url 'ftp://invisible-island.net/dialog/dialog.tar.gz'
      homepage 'http://invisible-island.net/dialog/'
      md5 '519c0a0cbac28ddb992111ec2c3f82aa'
      version '1.1.20070704'
    
      depends_on 'libiconv'
    
      def install
        system "./configure", "--disable-debug", "--disable-dependency-tracking",
                              "--prefix=#{prefix}"
        system "make install"
      end
    end

!SLIDE bullets
# __steps__
----
* <del>_search_</del>
* <del>_create_</del>
* <del>_edit (meta, build, dependencies)_</del>
* **test**
* pull request

!SLIDE
#    $ brew install -vd foo


!SLIDE
# default man page is 
# top levelfolder

!SLIDE smaller
# __--mandir__
----
    @@@ Ruby
      def install
        # Note: default man page is top levelfolder, added --mandir
        system "./configure", "--disable-debug", "--disable-dependency-tracking",
                              "--prefix=#{prefix}", "--mandir=#{man}"
        system "make install"
      end


!SLIDE bullets
# __steps__
----
* <del>_search_</del>
* <del>_create_</del>
* <del>_edit (meta, build, dependencies)_</del>
* <del>test</del>
* **pull request**

!SLIDE bullets
# __pull request__
---
* fork
* `$ git checkout --branch dialog`
* `$ cp /usr/local/Library/Formula/dialog.rb path/to/homebrew/Library/Formula`
* pull request

!SLIDE smaller
    @@@ Ruby
    require 'formula'
    
    class Dialog <Formula
      url 'ftp://invisible-island.net/dialog/dialog.tar.gz'
      homepage 'http://en.wikipedia.org/wiki/Dialog_(software)'
      # wikipedia page is more complete than (and contains link to)
      # homepage 'http://invisible-island.net/dialog/'
      md5 '519c0a0cbac28ddb992111ec2c3f82aa'
      version '1.1.20070704'
    
      # Listing from `otool -L /usr/local/bin/dialog`
      # 	/usr/lib/libncurses.5.4.dylib (compatibility version 5.4.0, current version 5.4.0)
      # 	/usr/lib/libiconv.2.dylib (compatibility version 7.0.0, current version 7.0.0)
      # 	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 125.2.0)
    
      depends_on 'libiconv'
      # TODO: review these dependencies
      # depends_on 'ncurses'
      # depends_on 'System'
    
      def install
        # Note: default man page is top levelfolder, added --mandir
        system "./configure", "--disable-debug", "--disable-dependency-tracking",
                              "--prefix=#{prefix}", "--mandir=#{man}"
        system "make install"
      end
    end


!SLIDE bullets
# __steps__
----
* <del>_search_</del>
* <del>_create_</del>
* <del>_edit (meta, build, dependencies)_</del>
* <del>test</del>
* <del>pull request</del>

!SLIDE
# _psych_

!SLIDE
# `brew install libiconv`

!SLIDE
    $ otool -L /usr/local/bin/dialog
    /usr/local/bin/dialog:
    	/usr/lib/libncurses.5.4.dylib (compatibility version 5.4.0, current version 5.4.0)
    	/usr/local/Cellar/libiconv/1.13.1/lib/libiconv.2.dylib (compatibility version 8.0.0, current version 8.0.0)
    	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 125.2.0)

!SLIDE bullets small
# __feedback__
----
* "Please use the proper homepage rather than wikipedia."
* "Those dependencies both come already with OSX so don't worry."
* "Please remove all the comments as a result."


!SLIDE smaller
    @@@ Ruby
    require 'formula'

    class Dialog <Formula
      url 'ftp://invisible-island.net/dialog/dialog.tar.gz'
      homepage 'http://invisible-island.net/dialog/'
      md5 '519c0a0cbac28ddb992111ec2c3f82aa'
      version '1.1.20070704'
    
      depends_on 'libiconv'
    
      def install
        # Note: default man page is top levelfolder, added --mandir
        system "./configure", "--disable-debug", "--disable-dependency-tracking",
                              "--prefix=#{prefix}", "--mandir=#{man}"
        system "make install"
      end
    end

!SLIDE
#surprise !

## The new commit is *already*
## in the pull request.

!SLIDE
# Done?

!SLIDE
# "Can I get those commits squished?"

!SLIDE
# __mxcl__.github.com/__homebrew__/
# wiki: Formula-Cookbook
----
# github.com/__mattscilipoti__/
# showoff_brew_your_own
---
# _@mattscilipoti_
