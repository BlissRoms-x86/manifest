<img src="https://i.imgur.com/0GnrwaU.png">

Bliss-ROM
-----------------------
Download the Bliss-ROM source code, based on [AOSP](https://android.googlesource.com), [phhusson](https://github.com/phhusson/treble_manifest), [skunkworx](https://github.com/skunkworkx/platform_manifest), & [BlissRoms](https://github.com/BlissRoms/platform_manifest)

---------------------------------------------------

Please read the [AOSP building instructions](http://source.android.com/source/index.html) before proceeding.

-----------------------
What you need to build [Bliss-ROM](https://github.com/BlissROMs/platform_manifest)
-----------------------

    Latest Ubuntu LTS Releases https://www.ubuntu.com/download/server
    Decent CPU (Dual Core or better for a faster performance)
    8GB RAM (16GB for Virtual Machine)
    250GB Hard Drive (about 170GB for the Repo and then building space needed)
  
-----------------------

Installing Java 8

    sudo add-apt-repository ppa:openjdk/ppa
    sudo apt-get update && upgrade
    sudo apt-get install openjdk-8-jdk
    update-alternatives --config java  (make sure Java 8 is selected)
    update-alternatives --config javac (make sure Java 8 is selected)
    reboot
    
-----------------------

Grabbing Dependencies
-----------------------

    $ sudo apt-get install git-core gnupg flex bison maven gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386  lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip squashfs-tools python-mako libssl-dev ninja-build lunzip syslinux syslinux-utils gettext genisoimage gettext bc xorriso

Initializing Repository
-----------------------

Repo initialization :
    
    ## Releases Repo ##
    $ repo init -u https://github.com/BlissRoms-x86/manifest.git -b p9.0-x86

sync repo :

    $ repo sync --no-tags --no-clone-bundle
    
problems syncing? :

    $ repo sync --no-tags --no-clone-bundle --force-sync

Building
--------

PC builds (x86) explained:
	  
	  This will build an x86 based .ISO for PCs

	  Usage: $ bash build-x86.sh options buildVariants blissBranch extraOptions
	  Options: -c | --clean : Does make clean && make clobber and resets the efi device tree
	    	   -s | --sync: Repo syncs the rom (clears out patches), then reapplies patches to needed repos
		   -p | --patch: Just applies patches to needed repos
		   -r | --proprietary: build needed items from proprietary vendor (non-public)

	  BuildVariants:
		android_x86-user : Make user build
		android_x86-userdebug |: Make userdebug build
		android_x86-eng : Make eng build
		android_x86_64-user : Make user build
		android_x86_64-userdebug |: Make userdebug build
		android_x86_64-eng : Make eng build

          BlissBranch: select which bliss branch to sync, default is p9.0

          ExtraOptions:
            	foss : packages microG & FDroid with the build
            	go : packages Gapps Go with the build
            	gapps : packages OpenGapps with the build
            	gms : packages GMS with the build (requires private repo access)
            	none : force all extraOption flags to false. 

	 To start, you must first use the -s (--sync) flag, then on following builds, it is not needed. 
	 Initial generation of the proprietary files from ChromeOS are also needed on the first build. 
	 We are able to use the -r (--proprietary) flag for that. This step needs to be on its own because
	 the mounting process requires root permissions, so keep a look out for it asking for your root password. 
	  
	 First you must sync with the new manifest changes:

        	$ bash build-x86.sh -p (will do initial patching)
	  
	 Next step is to download the proprietary files from ChromeOS:
	  
        	$ mkdir vendor/bliss_priv/proprietary && mkdir vendor/bliss_priv/source	    
        	$ bash build-x86.sh -r android_x86_64-userdebug 
	    
	 After that, you can build your release file:
	  
        	$ bash build-x86.sh android_x86_64-userdebug (to build the userdebug version for x86_64 CPUs)

