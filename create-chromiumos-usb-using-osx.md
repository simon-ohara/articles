# Installing ChromiumOS on an old laptop

The old laptop I was installing on was a [Toshiba Satellite C660D](http://www.toshiba.co.uk/discontinued-products/satellite-c660d-19x/)

## Create a Bootable Flash Drive

The first step is to create a bootable flash drive of ChromiumOS so that we can configure it for the old laptop.

### Get a ChromiumOS Image

Download a `<<zipped-image>>` of the [latest build](http://chromium.arnoldthebat.co.uk/index.php?dir=daily/&sort=date&order=desc) from **Arnold The Bat**. Make sure you select the correct architecture type for your old laptop. Mine was a 64bit machine so I selected the latest `Camd64OS` build. There are specific builds available for ARM and 32bit architectures.

Unzip the image using [p7zip](http://superuser.com/a/667076/402128)
```
$ cd Development/
$ mkdir ChromiumOS
$ cd ChromiumOS
$ 7z x ~/Downloads/<<zipped-image>>.7z
```

You will now have an `<<image-file>>.img`

### Install the image onto a flash drive

Plug in your flash drive ensure you can read/write to it. **The drive should be atleast 4Gb.**

Find the BSD file identifier for the flash drive to get `<<image-destination>>`
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

Use the `dd` command to install the image onto the flash drive. In this example `<<image-destination>>` is `disk2`. **WARNING** this will erase all existing data on the targetted volume - in this case the entire flash drive.
```
$ sudo dd if=<<image-file>>.img of=/dev/<<image-destination>>
```

This may take some time depending on the spec of you Mac. Mine took around 50/60mins to complete.

## Booting into ChromiumOS from the flash drive

Once the image installation is complete you can plug your flash drive into the old laptop. Turn on / reboot and enter the Boot List or Setup menus (F12 / F2 depending on BIOS). Select USB as the boot drive.

On first run Chromium takes you through a few setup steps. The first is selecting your language and keyboard layout, together with you preferred network (as almost everything in UI thereafter requires a connection to the internet). In my case a relevant driver for wifi didnt come with the image and so I was unable to select a network. If you are experiencing something similar you have two options (besides building your own ChromiumOS image):

1. Connect to a router with an ethernet cable
2. Skip setup and log in as Guest

Connecting with an ethernet cable allows you to complete setup but you will still have no wifi. To make this worth installing to the hard drive you will need to install the drivers for the wifi.

### Find out whats missing

Luckily, ChromiumOS will be telling us all of the problems it is having running on the hardware configuration of the old laptop. To view this you will need to enter Terminal mode:

1. Press `Ctrl+Alt+F2`
2. Type `chronos` and hit `Enter`
3. Type `password` and hit `Enter`

Use the `dmesg` command wrtie out the logs to a file.
```
$ touch Downloads/dmesg-output.txt
$ dmesg > Downloads/dmesg-output.txt
```

Press `Ctrl+Alt+F1` to return to GUI mode.

Open the file and search (`Ctrl+F`) for `wifi`.


### Installing drivers

The Chromium Open Source Project has loads of great developers contributing handy pieces of code that can be used to configure instances of ChromiumOS. Hardware drivers are one thing that you may need to add to your image that are specific to your old laptop.



