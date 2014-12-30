## Creating 


Install p7zip
http://superuser.com/a/667076/402128


Download latest build (from Arnold The Bat)
http://chromium.arnoldthebat.co.uk/index.php?dir=daily%2F


Unzip Image
```
cd Development/
mkdir ChromeOS
cd ChromeOS
7z x ~/Downloads/<<downloaded-zipped-image>>.7z
```

You now have an `<<image-file>>.img`

We now want to install this image onto a USB Flash Drive

Ensure the flash drive is connected

Find BSD file identifier for the flash drive to get `<<image-destination>>`
```
diskutil list

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

Install onto USB drive
`sudo dd if=<<image-file>>.img of=/dev/<<image-destination>>`

This may take some time depending on the spec of you Mac. Mine took arounf 50/60mins to complete.



