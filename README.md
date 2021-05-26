<img src="https://i.imgur.com/pOad4eK.png">

Bliss OS
-----------------------
Download the BlissRoms source code, based on [AOSP](https://android.googlesource.com), [phhusson](https://github.com/phhusson/treble_manifest) & [BlissRoms](https://github.com/BlissRoms/platform_manifest)

---------------------------------------------------

Please read the [AOSP building instructions](http://source.android.com/source/index.html) before proceeding.

-----------------------
What you need to build [BlissRoms](https://github.com/BlissROMs/platform_manifest)
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

    $ sudo apt-get install git-core gnupg flex bison maven gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip squashfs-tools python-mako libssl-dev ninja-build lunzip syslinux syslinux-utils gettext genisoimage gettext bc xorriso libncurses5 xmlstarlet build-essential git imagemagick lib32readline-dev lib32z1-dev liblz4-tool libncurses5-dev libsdl1.2-dev libxml2 lzop pngcrush rsync schedtool python-enum34 python3-mako libelf-dev


Initializing Repository
-----------------------

Repo initialization :
    
    ## Releases Repo ##
    $ repo init -u https://github.com/BlissRoms-x86/manifest.git -b r11-r36

sync repo :

    $ repo sync -c --force-sync --no-tags --no-clone-bundle -j$(nproc --all) --optimized-fetch --prune
    
Options
--------
	NO_KERNEL_CROSS_COMPILE - For some kernels, we use gcc-10 to compile. And some setups will require this flag to be added to compile the kernel properly. 
	BLISS_BUILD_VARIANT - (vanilla, gapps, foss) - We currently use this to specify what type of extra apps and services to iunclude in the build. 
	
Building
--------
    $ . build/envsetup.sh
    $ lunch android_x86_64-userdebug
    $ export NO_KERNEL_CROSS_COMPILE=true
    $ export BLISS_BUILD_VARIANT=foss
    $ mka iso_img

Extras
------
For many cases, we do offer a number of "extras" that can be compiled into the builds :

	*libndk-translation* - This is the ARM/ARM64 native-bridge we use in our builds. It will require some setup to include. See the project readme. - https://gitlab.com/android-generic/android_vendor_google_emu-x86
	*gapps* - USE_EMU_GAPPS=true (combine with BLISS_BUILD_VARIANT=gapps) - from Googles emulator images - Also included in https://gitlab.com/android-generic/android_vendor_google_emu-x86
	*houdini* - This is another ARM/ARM64 native-bridge we can use in our builds. It will require some setup to include. See the project readme. - https://github.com/BlissRoms-x86/android_vendor_google_chromeos-x86
	*Gearlock* - This is the recovery of choice for Android-x86 based builds. To include in builds: git clone https://github.com/axonasif/gearlock vendor/gearlock
	*Boringdroid* - We include the needed commits for all Boringdroid addons in Bliss. To include those into the builds: git clone https://github.com/boringdroid/vendor_boringdroid vendor/boringdroid && git clone https://github.com/boringdroid/vendor_prebuilts_bdapps vendor/prebuilts/bdapps
	
