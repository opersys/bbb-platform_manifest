# Downloading the sources

Make sure the `repo` tool is setup as it is described here:

https://source.android.com/setup/build/downloading#installing-repo

Create a directory for holding the sources and then initialize that repository:

```
mkdir -p ~/BBB-Android
cd ~/BBB-Android
```

then initialize with our default.xml:

```
repo init -u https://https://github.com/opersys/bbb-platform_manifest/ -b bbb
```

The name choosen for the directory does not matter. 

In that same directory, fetch the sources:

```
repo sync -j $(getconf _NPROCESSORS_ONLN)
```

# Building

From the directory you created in the steps above, prepare the environment for the build:

```
source build/envsetup.sh
```

Run lunch, to configure the build for your target.:

```
lunch beagleboneblack_sd-eng
```

(eventually, the ```beagleboneblack_emmc``` target will also be supported)

To build the sources:

```
./build-beagleboneblack.sh
```

## Writing to an SD-card

The writing script currently assume a 4GB MicroSD. We'll be working on adapting the build scripts to bigger cards in the future. The whole content of the card will be erased by this procedure.

DEVICE_NAME here is the filename of the device which corresponds to the MicroSD card. Ie: if the card corresponds to the ```/dev/sdc```, write just ```sdc``` there and not the whole path.

```
scripts/write-sdcard-beagleboneblack.sh $(DEVICE_NAME)
```

## Using the eMMC storage

We're still working on getting Android to boot from the eMMC storage.
