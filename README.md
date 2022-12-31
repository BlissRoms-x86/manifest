## What you need to build BlissOS

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

## Grabbing Dependencies

sudo apt-get install git gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386  lib32ncurses-dev x11proto-core-dev libx11-dev lib32z1-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip squashfs-tools python3-mako libssl-dev ninja-build lunzip syslinux syslinux-utils gettext genisoimage gettext bc xorriso xmlstarlet meson glslang-tools bison build-essential libncurses5 lib32ncurses5-dev
lib32ncurses5-dev

## Initializing Repository

**Repo initialization**
   
    repo init -u https://github.com/AndroidOS-PRO/BlissOS/manifest.git -b arcadia-x86

**Sync repo**

    repo sync -c --force-sync --no-tags --no-clone-bundle -j$(nproc --all) --optimized-fetch --prune

## Options

	BLISS_BUILD_VARIANT - (vanilla, gapps, foss) - We currently use this to specify what type of extra apps and services to include in the build. 
***Note: Default BLISS_BUILD_VARIANT is VANILLA.***

## Setup FOSS apps (if you choose to build FOSS)
----------------------------

- If you want to build with FOSS (this will include microG Services & some extra apps), go to vendor/foss and then type
```
    ./update.sh
```
And then choose 1 (x86/x86_64) to fetch all the apps. If you want to include Bromite Webview in, type this instead
```
    ./update.sh "" bromite
```
## Building

. build/envsetup.sh
lunch bliss_x86_64-userdebug export 
BLISS_BUILD_VARIANT=gapps
make iso_img
     
***Adding build options***

Before running `lunch`, you can add variables into the build to integrate more stuff into the image.
Note that you can put different variables into the build.

- **To build with FOSS**
```
    export BLISS_BUILD_VARIANT=foss
```

- **To build with [MindTheGapps](https://gitlab.com/MindTheGapps/vendor_gapps)**
```
export BLISS_BUILD_VARIANT=gapps
```
**More build options will be in Extras part including proprietary native-bridge/widevine libraries**

Extras
-------

We do offer some extra libraries that can be compiled into the build. These include :

***Prebuilt Widevine from Windows Subsystem for Android***
```
git clone https://github.com/supremegamers/vendor_google_proprietary_widevine-prebuilt vendor/google/proprietary/widevine-prebuilt
```
The variable to activate this is `USE_WIDEVINE=true`

***Windows Subsystem for Android's libhoudini*** 
```
git clone https://github.com/supremegamers/vendor_intel_proprietary_houdini vendor/intel/proprietary/houdini
```
The variable to activate this is `ANDROID_USE_INTEL_HOUDINI=true`

***GearLock Recovery*** 
```
git clone https://github.com/AXIM0S/gearlock vendor/gearlock
```

## Report build issues
- You can reach us via [Telegram Android™ (x86 PC) DEV](https://t.me/Android_X86_BY_DEDSECPRO)
