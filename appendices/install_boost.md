# Post-carpentry installation Instructions

This document contains instructions for installation of the Boost library tool

## Linux Users ##

Install the appropriate package with apt-get or yum, for example:

``` Bash
sudo apt-get install boost
```

## Mac Users ##

``` Bash
brew install boost
```

## Windows Users ##

You will need to download and install boost manually.

Create an appropriate folder, somewhere near your working code for the course.

For example, if you are working in `/home/myusername/devel/cppcourse/rsd-cppcourse/reactor` you could do:

``` Bash
mkdir -p ~/devel/libraries/boost
cd ~/devel/libraries/boost
```

Now, download and unzip boost, which will take quite a while:

```
curl -L http://sourceforge.net/projects/boost/files/boost/1.54.0/boost_1_54_0.zip/download > boost.zip
unzip boost.zip
```

Now, before we next build, we will need to tell our shell where the boost library can be found

```Bash
export CMAKE_INCLUDE_PATH = /home/myusername/devel/libraries/boost_1_54_0
```

... or your equivalent.