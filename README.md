<img src="https://i.imgur.com/pOad4eK.png">

Bliss-OS (x86) 12.x - BlissROM for PCs
-----------------------

Download the Bliss-OS source code, based on Andoid 10 using commits from [AOSP](https://android.googlesource.com), [Android-x86](https://android-x86.org), [Project Celadon](https://github.com/projectceladon), [phhusson](https://github.com/phhusson/treble_manifest), [skunkworx](https://github.com/skunkworkx/platform_manifest), & [BlissRoms](https://github.com/BlissRoms/platform_manifest)

---------------------------------------------------

Please read the [AOSP building instructions](http://source.android.com/source/index.html) before proceeding.

-----------------------
What you need to build [Bliss-OS](https://github.com/BlissROMs-x86/manifest)
-----------------------

    Latest [Ubuntu LTS Releases](https://www.ubuntu.com/download/server), Debian, Mint, [Bliss-Linux](https://sourceforge.net/projects/blissroms/files/Linux/) or the likes
    Decent CPU (Dual Core or better for a faster performance)
    8GB RAM (16GB for Virtual Machine)
    250GB Hard Drive (about 170GB for the Repo and then building space needed)
  
-----------------------

Installing Java 8 (if needed)

First, find out if you even need it:

    java --version
    
Depending on if it finds anything, you might need to install it:

    sudo add-apt-repository ppa:openjdk/ppa
    sudo apt-get update && upgrade
    sudo apt-get install openjdk-8-jdk
    update-alternatives --config java  (make sure Java 8 is selected)
    update-alternatives --config javac (make sure Java 8 is selected)
    reboot
    
-----------------------

Grabbing Dependencies
-----------------------

    $ sudo apt-get install git-core gnupg flex bison maven gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386  lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip squashfs-tools python-mako libssl-dev ninja-build lunzip syslinux syslinux-utils gettext genisoimage gettext bc xorriso libncurses5

You will also need to install enum34 for Python

    $ pip install enum34
-----------------------

Setting Up Environment Variables
-----------------------

Start off by adding these lines to your .bashrc file:

    ccache -F 0 && ccache -M 0 
	export PATH=~/bin:$PATH
	export CCACHE_DIR=/home/electrikjesus/.ccache
	export USE_CCACHE=1 
	export CCACHE_TEMPDIR=/tmp 
	export EXPERIMENTAL_USE_JAVA8=true 




Initializing Repository
-----------------------

Repo initialization :
    
    ## Releases Repo ##
    $ repo init -u https://github.com/BlissRoms-x86/manifest.git -b q10-x86

sync repo :

    $ repo sync --no-tags --no-clone-bundle -c
    
problems syncing? :

    $ repo sync --no-tags --no-clone-bundle --force-sync -c

Building
--------

To start, you must first sync or use the -s (--sync) flag, then on following builds, it is not needed. 

You can do this two ways. Traditionally or using the build script. Point is, you must sync with the new manifest changes. 

First Step is to Sync :

	$ repo sync --no-tags --no-clone-bundle --force-sync -c

Next step is to setup the build environment:

	$ . build/envsetup.sh

Then use the build scripts Patching method (-p) :

	$ build-x86 -p

Initial extraction of the proprietary files from Google are also needed on the first build. 
Please note that this process will need to be run for x86 & x86_64 builds seperately (some cleanup may be needed). 

We are able to use the -r (--proprietary) flag for that. This step needs to be done once per device setup (x86 or x86_64) and we have it working on its own because
the image mounting process requires root permissions, so keep a look out for it asking for your root password. 
	  	  
Next step is to download the proprietary files from Google :

	$ build-x86 -r android_x86_64-userdebug 

After that, you can build your release file :

	$ build-x86 android_x86_64-userdebug foss crosboth (to build the userdebug version for x86_64 CPUs with FDroid & microG included)


PC (x86) build script explained:
--------------------------------
	  
This script will allow you to build an x86 based .ISO for PCs as well as help you with a few other things. Please see details below

Usage :  

	$ build-x86 options buildVariants extraOptions addons

Options : 

	-c | --clean : Does make clean && make clobber and resets the device tree
	-s | --sync: Repo syncs the rom (clears out patches), then reapplies patches to needed repos
	-p | --patch: Just applies patches to needed repos
	-r | --proprietary: build needed items from proprietary vendor (non-public)

BuildVariants :

	android_x86-user : Make user build
	android_x86-userdebug |: Make userdebug build
	android_x86-eng : Make eng build
	android_x86_64-user : Make user build
	android_x86_64-userdebug |: Make userdebug build
	android_x86_64-eng : Make eng build

ExtraOptions : Defaults to None

	foss : packages microG & FDroid with the build
	fdroid : packages custom FDroid with the build (requires private sources)
	go : packages Gapps Go with the build (when go vendor is synced)
	gapps : packages OpenGapps with the build (when OpenGapps vendor sources are synced)
	gms : packages GMS with the build (requires private repo access)
	none : force all extraOption flags to false. (Default Option)

Addons : Requires "--proprietary" build to have run at least once. Defaults to None

	croshoudini : Include libhoudini from Chrome OS 
	croswidevine : Include widevine from Chrome OS
	crosboth : Include both libhoudini and widevine from Chrome OS
	crosnone : Do not include any of them. (Default Option)
