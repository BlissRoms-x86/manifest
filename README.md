<img src="https://imgur.com/jmiT0ss.png">
<p align="center">
<a href="https://blissroms.org">Website</a> |
<a href="https://downloads.blissroms.org">Download</a> |
<a href="https://www.paypal.com/donate/?hosted_button_id=J5SLZ7MQNCT24">Donate</a> |
<a href="https://docs.blissroms.org">Documentation</a> |
<a href="https://www.instagram.com/blissroms">Instagram</a> |
<a href="https://t.me/BlissROM_Updates">Telegram</a>

## BlissRoms

Download the BlissRoms source code, based on [AOSP](https://android.googlesource.com) & [BlissRoms](https://github.com/BlissRoms/platform_manifest)

---------------------------------------------------

Please read the [AOSP building instructions](http://source.android.com/source/index.html) before proceeding.

-----------------------
## What you need to build [BlissRoms](https://github.com/BlissROMs/platform_manifest)


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

    sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386  lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip squashfs-tools python-mako libssl-dev ninja-build lunzip syslinux syslinux-utils gettext genisoimage gettext bc xorriso xmlstarlet

## Initializing Repository

**Repo initialization**
   
    repo init -u https://github.com/BlissRoms/platform_manifest.git -b arcadia-next

**Sync repo**

    repo sync -c --force-sync --no-tags --no-clone-bundle -j$(nproc --all) --optimized-fetch --prune

## Options

	BLISS_BUILD_VARIANT - (vanilla, gapps, foss) - We currently use this to specify what type of extra apps and services to include in the build. 
***Note: Default BLISS_BUILD_VARIANT is VANILLA.***

## Building

     . build/envsetup.sh
     blissify options deviceCodename
     

**Options:**
```
-h | --help: Shows the help dialog
-c | --clean: Clean up before running the build
-d | --devclean: Clean up device only before running the build
-v | --vanilla: Build with no added app store solution **default option**
-g | --gapps: Build with Google Play Services added
-f | --foss: build with FOSS (arm64-v8a) app store solutions added **requires vendor/foss**
```

**Examples:**

- **To build with gapps**
```
     blissify -g deviceCodename
```

- **To build with FOSS**
```
     blissify -f deviceCodename
```

- **To build with gapps and deviceclean**
```
     blissify -g -d deviceCodename
```

**This method is also backwards compatible with the legacy blissify command also**
```
     blissify deviceCodename
```
## Report build issues
- You can reach us via [Telegram (BlissRoms Build Support)](https://t.me/Team_Bliss_Build_Support)
