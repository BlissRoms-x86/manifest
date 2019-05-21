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

    $ sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386  lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip squashfs-tools python-mako libssl-dev ninja-build lunzip syslinux syslinux-utils gettext genisoimage gettext bc xorriso

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
treble build options explained:

      Usage: $ bash build-treble.sh options buildVariants blissBranch
      options: -c | --clean : Does make clean && make clobber and resets the treble device tree
               -r | --release : Builds a twrp zip of the rom (only for A partition) default creates system.img
               -p | --patch: Just applies patches to needed repos
               -s | --sync: Repo syncs the rom (clears out patches), then reapplies patches to needed repos
      
      buildVariants: arm64_a_stock | arm64_ab_stock : Vanilla Rom
                      arm64_a_gapps | arm64_ab_gapps : Stock Rom with Gapps Built-in
                      arm64_a_foss | arm64_ab_foss : Stock Rom with Foss
                      arm64_a_go | arm64_ab_go : Stock Rom with Go-Gapps
      
      blissBranch: select which bliss branch to sync, default is p9.0
      
      First you must sync with the new manifest changes:
      
		$ bash build-treble.sh -s
      
      After the sync is finished, you can build your release:
      
        $ bash build-treble.sh -r arm64_a_gapps (to build armA 64bit with gapps built in)
      
Celadon EFI (Android-IA) build options explained:

      Usage: $ bash build-efi.sh options buildVariants blissBranch
      options: -c | --clean : Does make clean && make clobber and resets the efi device tree
               -s | --sync: Repo syncs the rom (clears out patches), then reapplies patches to needed repos
      
      buildVariants: user : Make user build
                      userdebug |: Make userdebug build
                      eng : Make eng build
      
      blissBranch: select which bliss branch to sync, default is p9.0

      After the sync is finished

        $ bash build-efi.sh -s userdebug (to build the userdebug version)

emulator builds explained:
  
      Precondition: android SDK must be installed in ~/Android/SDK

        $ lunch bliss_emulator-userdebug
        $ make

      if you want to run on the same host:

        $ bash vendor/bliss/utils/emulator/start_emulator_local.sh

      if you need to copy on a different host:

        $ vendor/bliss/utils/emulator/create_emulator_image.sh
        $ cp /tmp/bliss_emulator.zip to the device where you have installed android SDK
  
      (unzip into /tmp)

        $ bash /tmp/generic_x86/start_emulator_image.sh

PC builds (x86) explained:
	  
	  (WIP) Add x86 PC builds

	  This will build an x86 based .ISO for PCs

	  Usage: $ bash build-x86.sh options buildVariants blissBranch
	  Options: -c | --clean : Does make clean && make clobber and resets the efi device tree
	    	   -s | --sync: Repo syncs the rom (clears out patches), then reapplies patches to needed repos
			   -p | --patch: Just applies patches to needed repos
			   -r | --proprietary: build needed items from proprietary vendor (non-public)

	  BuildVariants: android_x86-user : Make user build
				     android_x86-userdebug |: Make userdebug build
				     android_x86-eng : Make eng build
				     android_x86_64-user : Make user build
				     android_x86_64-userdebug |: Make userdebug build
				     android_x86_64-eng : Make eng build

	  BlissBranch: select which bliss branch to sync, default is p9.0

	  To start, you must first use the -s (--sync) flag, then on following builds, it is not needed. 
	  Initial generation of the proprietary files from ChromeOS are also needed on the first build. 
	  We are able to use the -r (--proprietary) flag for that. This step needs to be on its own because
	  the mounting process requires root permissions, so keep a look out for it asking for your root password. 
	  
	  First you must sync with the new manifest changes:

	    $ bash build-x86.sh -s (will also do initial patching)
	  
	  Next step is to download the proprietary files from ChromeOS:
	  
	    $ bash build-x86.sh -r android_x86_64-userdebug 
	    
	  After that, you can build your release file:
	  
	    $ bash build-x86.sh android_x86_64-userdebug (to build the userdebug version for x86_64 CPUs)

