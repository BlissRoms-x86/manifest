<img src="https://i.imgur.com/0GnrwaU.png">

BlissRoms
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

    $ sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386  lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip squashfs-tools python-mako libssl-dev ninja-build lunzip syslinux syslinux-utils gettext genisoimage gettext bc xorriso xmlstarlet

Initializing Repository
-----------------------

Repo initialization :
    
    ## Releases Repo ##
    repo init -u https://github.com/BlissRoms/platform_manifest.git -b r

sync repo :

    repo sync -c --force-sync --no-tags --no-clone-bundle -j$(nproc --all) --optimized-fetch --prune

Building
--------
     . build/envsetup.sh
     blissify device-codename
    
