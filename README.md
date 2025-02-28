<img src="https://i.imgur.com/pOad4eK.png">

BlissOS
-----------------------
Download the BlissOS source code, based on [AOSP](https://android.googlesource.com), [Android-x86](https://www.android-x86.org/), [phhusson](https://github.com/phhusson/treble_manifest) & [BlissRoms](https://github.com/BlissRoms/platform_manifest)

<div align="center">
<strong><i>Modified for PC build using Android-Generic Project</i></strong>
<br>
<img src="https://i.ibb.co/rf2rv3M/Yep1l4L.png">
<br>
</div>

---------------------------------------------------

Please read the [AOSP building instructions](http://source.android.com/source/index.html) before proceeding.

-----------------------
What you need in order to build [BlissOS](https://github.com/BlissRoms-x86/manifest)
-----------------------

    Latest Ubuntu LTS Releases https://www.ubuntu.com/download/server
    Decent CPU (Dual Core or better for a faster performance)
    8GB RAM (16GB for Virtual Machine)
    250GB Hard Drive (about 170GB for the Repo and then building space needed)
  
Grabbing Dependencies
-----------------------

    sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386  lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip squashfs-tools python3-mako libssl-dev ninja-build lunzip syslinux syslinux-utils gettext genisoimage gettext bc xorriso xmlstarlet meson glslang-tools git-lfs libncurses5 libncurses5:i386 libelf-dev aapt zstd rdfind nasm

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

Initializing Repository
-----------------------

**Repo initialization**
    
    ## Releases Repo ##
    repo init -u https://github.com/BlissRoms-x86/manifest.git -b r11-x86 --git-lfs

**Sync repo**

    repo sync -c --force-sync --no-tags --no-clone-bundle -j$(nproc --all) --optimized-fetch --prune

Options
--------
	BLISS_BUILD_VARIANT - (vanilla, opengapps, foss) - We currently use this to specify what type of extra apps and services to iunclude in the build. 
***Note: Default BLISS_BUILD_VARIANT is VANILLA.***

    BLISS_SPECIAL_VARIANT - This can be custom set if you wanna build a version for a specific device 
    for example -jupiter for Steam Deck or -surface for Microsoft Surface series

Setup FOSS apps or OpenGapps
----------------------------

- If you want to build with FOSS (this will include microG Services & some extra apps), go to vendor/foss and then type
```
    ./update.sh
```
And then choose 1 (x86/x86_64) to fetch all the apps. If you want to include Bromite Webview in, type this instead
```
    ./update.sh "" bromite
```

- If you want to build with OpenGapps, first make sure to get `git-lfs` (already listed in above). Once you got `git-lfs`, type this
```
    repo forall -c git lfs pull
```
To fetch the packages.

Building
--------
    $ . build/envsetup.sh
    $ lunch bliss_x86_64-userdebug
    $ make iso_img
     
***Adding build options***

Before running `make iso_img`, you can adding variables into the build to integrate more stuff into the image.
Note that you can put different variables into the build.

- **To build with FOSS**
```
    export BLISS_BUILD_VARIANT=foss
```

- **To build with OpenGapps**
```
    export BLISS_BUILD_VARIANT=opengapps
```

- **To build with proprietary libhoudini extracted from WSA**
```
    export ANDROID_USE_INTEL_HOUDINI=true
```

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


**More build options will be in Extras part including proprietary native-bridge/widevine libraries**

Extras
-------

We do offer some extra libraries that can be compiled into the build. These include :

***ChromeOS's libhoudini/Widevine DRM L3*** 

https://github.com/supremegamers/android_vendor_google_chromeos-x86

Clone to `vendor/google/chromeos-x86`, go to the folder and open terminal
`./extract-files.sh`

The variable to activate this is `USE_CROS_HOUDINI_NB=true` for libhoudini and `USE_WIDEVINE=true` for Widevine.

***Prebuilt Widevine from Windows Subsystem for Android***

https://github.com/supremegamers/vendor_google_proprietary_widevine-prebuilt

Clone to `vendor/google/proprietary/widevine-prebuilt`, The variable to activate this is `USE_WIDEVINE=true`

***Windows Subsystem for Android's libhoudini*** 

https://github.com/supremegamers/vendor_intel_proprietary_houdini

Clone to `vendor/intel/proprietary/houdini`, The variable to activate this is `ANDROID_USE_INTEL_HOUDINI=true`
## Report build issues
- You can reach us via [Telegram (Android™-Generic (x86 PC) Community Development)](https://t.me/androidgenericpc)
