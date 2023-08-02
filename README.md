<img src="https://i.imgur.com/0nNfAQ8.png">
<p align="center">

## BlissBass

An Android-x86 variant designed to be rebranded and used for all types of use cases. 

- Menu driven customization options (Check the Vendor Customization Layer for more info)
- Generic boot process (allows for one OS to boot on many x86/x86_64 machines)
- Added features and options geared towards products and single-use displays

Download the BlissBass source code, based on [AOSP](https://android.googlesource.com), [Bliss OS](http://blissos.org/) & [Android-x86](http://android-x86.org/)

**!!WARNING!!** This project includes a [Vendor Customization Layer (vendor/branding)](https://github.com/BlissRoms-x86/platform_vendor_branding) that is free for testing and open-source development, but should be licensed for business or private use. 

---------------------------------------------------

Please read the [AOSP building instructions](http://source.android.com/source/index.html) before proceeding.

-----------------------
## What you need to build [BlissBass](https://github.com/BlissRoms-x86/manifest)


    Latest Ubuntu LTS Releases https://www.ubuntu.com/download/server
    Decent CPU (16 Cores or better for a faster performance)
    16GB RAM (32GB for Virtual Machine)
    350GB Hard Drive (about 170GB for the Repo and then building space needed)

    Time to compile:
    Laptop: 6-8 hours
    Desktop/Workstation: 4-6 hours
    Server: 1-2 hours

To setup under a VM, you can follow instructions to install Virtualbox and ubuntu for [Mac OS](https://medium.com/tech-lounge/how-to-install-ubuntu-on-mac-using-virtualbox-3a26515aa869) or [Windows](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview) 

-----------------------

## Grabbing Dependencies

```
    sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386  lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip squashfs-tools python3-mako libssl-dev ninja-build lunzip syslinux syslinux-utils gettext genisoimage gettext bc xorriso xmlstarlet meson glslang-tools git-lfs libncurses5 libncurses5:i386 libelf-dev aapt
```

## Initializing Repository

**Repo initialization**
```
    repo init -u https://github.com/BlissRoms-x86/manifest.git -b arcadia-bass --git-lfs
```

**Sync repo**
```
    repo sync -c -j4 --force-sync  --no-tags
```

## Options

This build is targeting a specific vendor, so we use the following options to export variables to the build environment before we run the lunch command and compile:
```
    . build/envsetup.sh 
    
    RELEASE_OS_TITLE="BlissBass" && export USE_SMARTDOCK=false && export USE_KERNEL_SU_PLUS=false && export USE_FOSSAPPS=false && export BLISS_BUILD_VARIANT=vanilla && export IS_GO_VERSION=false && export BLISS_SUPER_VANILLA=true && export USE_GO_RES_ICONS=false && export BLISS_SPECIAL_VARIANT=-preview-1
```

## Building
```
    lunch bliss_x86_64-userdebug
    make iso_img
```
