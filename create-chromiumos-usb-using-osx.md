# Installing Chromium OS on an old laptop

The old laptop I was installing on was a [Toshiba Satellite C660D](http://www.toshiba.co.uk/discontinued-products/satellite-c660d-19x/)

## Creating the Bootable Flash Drive

1. Install [p7zip](http://superuser.com/a/667076/402128)

2. Download a `<<zipped-image>>` of the [latest build](http://chromium.arnoldthebat.co.uk/index.php?dir=daily%2F) (from Arnold The Bat). Make sure you select the correct architecture type for your old laptop. Mine was a 64bit machine so I selected the latest `Camd64OS` build. There are specific builds available for ARM and 32bit architectures.

3. Unzip the image using p7zip
```
$ cd Development/
$ mkdir ChromiumOS
$ cd ChromiumOS
$ 7z x ~/Downloads/<<zipped-image>>.7z
```

You will now have an `<<image-file>>.img`

4. We now want to install this image onto a USB Flash Drive. Ensure you have one connected and that you can read/write to it. **The drive should be atleast 4Gb.**

5. Find BSD file identifier for the flash drive to get `<<image-destination>>`
```
$ diskutil list

/dev/disk0
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *500.3 GB   disk0
   1:                        EFI EFI                     209.7 MB   disk0s1
   2:          Apple_CoreStorage                         499.4 GB   disk0s2
   3:                 Apple_Boot Recovery HD             650.0 MB   disk0s3
/dev/disk1
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:                  Apple_HFS Macintosh HD           *499.1 GB   disk1
/dev/disk2
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *7.8 GB     disk2
   1:             Windows_FAT_32 USB2                    7.8 GB     disk2s1
```

In this example `<<image-destination>>` is `disk2`

6. Use the `dd` command to install the image onto the flash drive. **WARNING** this will erase all existing data on the targetted volume - in this case the entire flash drive.
```
$ sudo dd if=<<image-file>>.img of=/dev/<<image-destination>>
```

This may take some time depending on the spec of you Mac. Mine took around 50/60mins to complete.

## Running ChromiumOS

Once complete you can connect your USB to the machine on which you wish to run ChromiumOS. You will need to enter the Boot List or Setup menus to select USB as the boot drive so that it runs from the flash drive.

On first run Chromium takes you through a few setup steps. The first is selecting your language and keyboard layout, together with you preferred network (as almost everything in UI thereafter requires a connection to the internet). In my case a relevant driver for wifi didnt come with the image and so I was unable to select a network. If you are experiencing something similar you have two options (besides building your own ChromiumOS image):

1. Connect to a router with an ethernet cable
2. Use another USB drive to acquire the relevant drivers using a different machine





