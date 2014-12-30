## Creating 


Install [p7zip](http://superuser.com/a/667076/402128)


Download a `<<zipped-image>>` of the [latest build](http://chromium.arnoldthebat.co.uk/index.php?dir=daily%2F) (from Arnold The Bat)


Unzip the image using p7zip
```
$ cd Development/
$ mkdir ChromeOS
$ cd ChromeOS
$ 7z x ~/Downloads/<<zipped-image>>.7z
```

You will now have an `<<image-file>>.img`

We now want to install this image onto a USB Flash Drive. Ensure you have one connected and that you can read/write to it. **The drive should be atleast 4Gb.**

Find BSD file identifier for the flash drive to get `<<image-destination>>`
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

Use the `dd` command to install the image onto the flash drive. **WARNING** this will erase all existing data on the targetted volume - in this case the entire flash drive.
```
$ sudo dd if=<<image-file>>.img of=/dev/<<image-destination>>
```

This may take some time depending on the spec of you Mac. Mine took around 50/60mins to complete.



