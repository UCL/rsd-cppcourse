\appendix 

Installation Instructions
=========================

Introduction
------------

This document contains instructions for installation of the packages
we'll be using during the RITS Autumn 2013 C++ course.

If you have already followed the Software Carpentry instructions, you will have done most of this already. 

Just follow the [additional instructions](02extra_preparation.md) for installing Subversion and CMake.

Linux users should be able to use their package manager to install all software requirements, and should have C++ and a decent editor already.
(if you're using Linux, we assume you won't have any trouble with these requirements).

However note that if you are running an older Linux distribution you may get older versions with different look and features.
A recent Linux distribution is recommended. 

Mac and Windows users should follow the instructions below.

Give yourself 30 minutes or so to run through this installation process and don't get intimidated!
Please try to install everything well before the bootcamp,
as it is important that we don't waste time during the workshop trying to mend installations. 

If you do get stuck, first try searching on the internet (e.g. [stackoverflow.com](http://stackoverflow.com)) for solutions.
Or, try asking a fellow bootcamp attendee for help.

We will be running a drop-in session on the afternoon of Monday 23rd September from 13:00 - 17:00 in Room G07,
Chadwick Building (main campus on Gower Street) for people that would like some help with setting up their laptop in 
advance of the boot camp. All students should either attend this or ensure 
that they have a working git, python, and editor and shell installation by following the instructions bellow before the workshop. 

We will be using UCL's [eduroam](http://www.ucl.ac.uk/isd/staff/wireless/eduroam) service to connect to the internet for this work. 
So you should ensure you have eduroam installed and working.

## Linux Users ##

## Git ##

If git is not already available on your machine 
you can try to install it via your distribution package manager (e.g. `apt-get` or `yum`).

On ubuntu or other Debian systems:

    sudo apt-get install git

On RedHat based systems:

    yum install git

## Subversion ##

Again, install the appropriate package with apt-get or yum (`subversion`)

## CMake ##

Again, install the appropriate package with apt-get or yum (`cmake`)

## Editor and shell ##

Many different text editors suitable for programming are available.
If you don't already have a favourite,
you could look at [Kate](http://kate-editor.org/).

Regardless of which editor you have chosen you should configure git to use it. Executing something like this in a terminal should work:

```
git config --global core.editor NameofYourEditorHere
```

The default shell is usually bash but if not you can get to bash by opening a terminal and typing `bash`.

## Mac Users ##

## XCode and command line tools ##

Install [XCode](https://itunes.apple.com/us/app/xcode/id497799835) using the Mac app store. 

Then, go to Xcode...Preferences...Downloads... and install the command line tools option

## Git ##

Install Homebrew via typing this at a terminal:

``` Bash
ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"
```    

and then type

``` Bash
brew install git
```


Then install the [GitHub for Mac client](http://mac.github.com).

## CMake

Just do

``` Bash
brew install cmake
```

## Editor and shell ##

The default text editor on OS X *textedit* should be sufficient for our use. Alternatively 
http://mac.appstorm.net/roundups/office-roundups/top-10-mac-text-editors/ lists a number of other good editors. 

To setup git to use *textedit* executing the following in a terminal should do.

``` Bash
git config --global core.editor /Applications/TextEdit.app/Contents/MacOS/TextEdit
```

The default terminal on OSX should also be sufficient. If you want a more advanced terminal [iTerm2](http://www.iterm2.com/) is an alternative.

## Windows Users ##

## Git ##

Install [msysgit](http://code.google.com/p/msysgit/downloads/list?q=full+installer+official+git)

Then install the [GitHub for Windows client](http://windows.github.com/).

## Subversion

Install [subversion](http://sourceforge.net/projects/win32svn/)

And choose to add it to the path for all users if so prompted.

## CMake

Install [cmake](http://www.cmake.org/cmake/resources/software.html)

And choose to add it to the path for all users if so prompted.

## Editor ##

Unless you already use a specific editor which you are comfortable with we recommend using 
[*Notepad++*](http://notepad-plus-plus.org/) on windows.

Using Notepad++ to edit text files including code should be straight forward but in addition you should configure git 
to use notepad++ when writing commit messages (We will learn about these in the version controle session).   

## Unix tools ##

Install [MinGW](http://sourceforge.net/projects/mingw/) by following the download link.
It should install MinGW's package manager. On the left, select ``Basic Setup``, and on right select
``mingw32-base, mingw-developer-toolkit, mingw-gcc-g++, msys-base``. On some systems these package
might be selected from start. Finally, click the installation menu and ``Apply Changes``. 

Now, we need to find out where Git and Notepad++ have been installed, this will be either in 
`C:/Program Files (x86)` or in `C:\ProgramFiles`. The former is the norm on more modern versions of windows.
If you have the older version, replace `Program\ Files\ \(x86\)` with `Program\ Files` in the instructions below.

We need to tell the new shell installed in this way where git and Notepad++ are.

To do this, use NotePad++ to edit the file at `C:\MinGW\mysys\1.0\etc\profile`

and toward the end, above the line `alias clear=clsb` add the following:

 ``` Bash
# Path settings from SoftwareCarpentry
export PATH=$PATH:/c/Program\ Files\ \(x86\)/Git/bin
export PATH=$PATH:/c/Program\ Files\ \(x86\)/Notepad++
# End of Software carpentry settings
```

Check this works by opening MinGW shell, with the start menu (Start->All programs->MinGW->MinGW
Shell). This should open a *terminal* window, where commands can be typed in directly. On windows 8,
there may be no app for MinGW. In that case, open the ``run`` app and type in
``C:\MinGW\msys\1.0\msys.bat``. Once you have a terminal open, type

``` Bash
which notepad++
```

which should produce readout similar to `/c/Program Files (x86)/Notepad++/notepad++.exe`

``` Bash
which git
```

which should produce `/c/Program Files (x86)/Notepad++/notepad++.exe`. The ``which`` command is used
to figure out where a given program is located on disk.

Now we need to update the default editor used by Git.

``` Bash
git config --global core.editor "'C:/Program Files (x86)/Notepad++/notepad++.exe' 
	-multiInst  -nosession -noPlugin"
```

Note that it is not obvious how to copy and paste text in a Windows terminal including Git Bash.
Copy and paste can be found by right clicking on the top bar of the window and selecting the
commands from the drop down menu (in a sub menu).  

You should now have a working version of git and notepad++, accessible from your shell.

If you have problems following these instructions, please come to our drop-in session on Monday 23rd September, 1-5, 
G07 Chadwick building.
