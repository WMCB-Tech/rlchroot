Please note that i'm not maintaining devices with older versions of Android as Termux ended support for outdated android versions

Currently the reason why i only chose to maintain Android 7 upto 10/11 versions is:
* Changes in `proot` are integrated with the environment
* Easier to manage
* Fix SELinux Problems

For those people who need to use `rlchroot` (For bug fixes and for testing), you will need to backport `proot` package in order to keep it up to date)

You need to download `proot` debian package here:
https://dl.bintray.com/termux/termux-packages-24/

And you need to find `proot` package and install it

`libtalloc` dependency is also required however you can just install it with `apt install libtalloc`
