<img src="banner.png">
<p align="center">
<a href="https://https://blissos.org">Website</a> |
<a href="https://sourceforge.net/projects/blissos-x86">Download</a> |
<a href="https://www.paypal.com/donate/?hosted_button_id=J5SLZ7MQNCT24">Donate</a> |
<a href="https://docs.blissos.org/">Documentation</a> |
<a href="https://t.me/blissx86">Telegram</a>

## BlissOS

Download the BlissOS source code, based on [AOSP](https://android.googlesource.com) & [Android-x86](http://android-x86.org/)

<div align="center">
<strong><i>Modified for PC build using Android-Generic Project</i></strong>
<br>
<img src="https://i.ibb.co/rf2rv3M/Yep1l4L.png">
<br>
</div>

---------------------------------------------------

Please read the [AOSP building instructions](http://source.android.com/source/index.html) before proceeding.

-----------------------
## What you need to build [BlissOS](https://github.com/BlissRoms-x86/manifest)


    Latest Ubuntu LTS Releases https://www.ubuntu.com/download/server
    Decent CPU (Dual Core or better for a faster performance)
    24GB RAM (30GB for Virtual Machine)
    250GB Hard Drive (about 170GB for the Repo and then building space needed)
  
-----------------------

## Grabbing Dependencies

    sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386  lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip squashfs-tools python3-mako libssl-dev ninja-build lunzip syslinux syslinux-utils gettext genisoimage gettext bc xorriso xmlstarlet meson glslang-tools git-lfs libncurses5 libncurses5:i386 libelf-dev aapt zstd rdfind nasm kmod

    Rust toolchain & programs are also required. We recommend you to install them using rustup !
    First, remove distro' Rust toolchain:
    sudo apt remove rustc bindgen cargo -y
    
    Next install rustup by following this page:
    https://www.rust-lang.org/tools/install

    After getting rustup installed, install required programs & toolchain:
    cargo install cargo-ndk
    rustup target add x86_64-linux-android i686-linux-android
    cargo install --version 0.69.1 bindgen-cli
    cargo install cbindgen

## Initializing Repository

**Repo initialization**
   
    repo init -u https://github.com/BlissOS/platform_manifest.git -b voyager-x86 --git-lfs

**Sync repo**

    repo sync -c --force-sync --no-tags --no-clone-bundle -j$(nproc --all) --optimized-fetch --prune

## Options

	BLISS_BUILD_VARIANT - (vanilla, gapps, foss, microg) - We currently use this to specify what type of extra apps and services to include in the build. 
***Note: Default BLISS_BUILD_VARIANT is VANILLA.***

   BLISS_SPECIAL_VARIANT - This can be custom set if you wanna build a version for a specific device 
    for example `-jupiter` for Steam Deck or `-surface` for Microsoft Surface series

## Building

    $ . build/envsetup.sh
    $ lunch bliss_x86_64-ap4a-userdebug
    $ make iso_img
     
***Adding build options***

Before running `lunch`, you can add variables into the build to integrate more stuff into the image.
Note that you can put different variables into the build.

- **To add a custom label into a device-specific build**
```
    export BLISS_SPECIAL_VARIANT=-Jupiter
```

- **To build the special "surface" variant which include kernel with patches from linux-surface and the iptsd userspace touchscreen daemon**
```
    export BOARD_IS_SURFACE_BUILD=true
```

- **To build the special "go" variant for BlissOS Go**
```
    export BOARD_IS_GO_BUILD=true
```

- **To build the special "zenith" variant for BlissOS Zenith**
```
    export BOARD_IS_ZENITH_BUILD=true
```

## Report build issues
- You can reach us via [Telegram (Android™-Generic (x86 PC) Community Development)](https://t.me/androidgenericpc)
