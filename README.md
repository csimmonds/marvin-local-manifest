# Marvin: creating a minimal AOSP device

## Why Marvin?

Marvin demonstrates how to construct a minimal device on AOSP. It is based on
the Android Cuttlefish emulator [1] built for the x86 architecture. Marvin
is available in two flavours: vanilla and car

This version is based on AOSP 12

The name, Marvin, comes from the Hitchhiker's Guide to the Galaxy, by Douglas Adams. Marvin
is a paranoid android, and he was manufactured by the Sirius Cybernetics
Corporation.

## Preparation

Make sure that you have a system capable of building AOSP in a reasonable
amount of time, as described here...

[https://source.android.com/source/building.html](https://source.android.com/source/building.html).

...and here

[https://source.android.com/source/initializing.html](https://source.android.com/source/initializing.html)


## Download AOSP

Choose a directory for the AOSP source, e.g. $HOME/aosp:
```
$ mkdir ~/aosp && cd ~/aosp
```

Select the release of AOSP 12 you want, e.g. r26:
```
$ repo init -u https://android.googlesource.com/platform/manifest -b android-12.0.0_r26
$ repo sync -c
```
The total download will be about 115 GB

If you don't care too much about the git history you can reduce the download by
about 48 GB by doing doing a shallow clone like this:
```
$ repo init --depth=1 -u https://android.googlesource.com/platform/manifest -b android-12.0.0_r26
```

Get Marvin and sync
```
$ cd ~/aosp
$ git clone https://github.com/csimmonds/marvin-local-manifest .repo/local_manifests -b android12
$ repo sync -c
```

## Build AOSP

```
$ cd ~/aosp
$ source build/envsetup.sh
```
For vanilla marvin, i.e. to build a phone:
```
$ lunch marvin-userdebug
```

For marvincar, i.e. to build Andoid Automotive OS:
```
$ lunch marvincar-userdebug
```

Then set the build running by typing 'm'
```
$ m
```
The command 'm' is a wrapper for 'make', with the additional benefit that it
will use all available CPU cores (see ~/aosp/build/soong/ui/build/config.go).

Even so, the build will take a few hours

