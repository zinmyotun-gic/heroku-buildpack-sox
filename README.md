Heroku buildpack: sox
=======================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for using [sox](http://sox.sourceforge.net/) in your project.  

Lineage
-------

Shamelessly forked from the [ffmpeg heroku buildpack](https://github.com/shunjikonishi/heroku-buildpack-ffmpeg) by [Shunji Konishi](https://github.com/shunjikonishi).

Usage
-----
As of 2020, the multi-buildpack concept is no longer recommended by Heroku.  In this case, I was able to get SOX 14.4.2 compiled and running in my service through the following:

    $ heroku create 
    Creating app...
    
    $ heroku buildpacks:add --index 1 https://github.com/tgmerritt/heroku-buildpack-sox.git

    $ git add 
    $ git commit -m "message here"
    $ git push heroku master
    ...

You can verify that sox is installed by calling:

    $ heroku run "sox"

Notes
-----

The original project from [lepinsk](https://github.com/lepinsk/heroku-buildpack-sox) must have used an older version of SOX, and certainly the Linux version that Heroku runs on (as of 2020) is newer.  This created a number of conflicts in the `bin/compile` file between this version and the original.  If you are finding this buildpack in the future, and SOX isn't compiling for you on whatever version of Heroku is running at that time, you need to check the deployment logs and see if there are error messages such as `bash: sox command not found` or `unable to locate libblah.so - file not found` - these errors indicate that SOX was never installed (in the first instance) and that certain paths which are declared in the `bin/compile` file are no longer correct for whatever future version of this library you're running.

I wasn't sure which version of SOX was included in the original - it's still in this repo as `sox.tar.gz.old` but I pulled the latest from a Linux distro server (14.4.2 as of this writing) and put that in place within this repo.  So if it's 5 years in the future when you find this, you'll probably need to grab a newer version of SOX and fork this repo to make it all work ok.