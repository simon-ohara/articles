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

Find out the file of the USB Drive


Install onto USB drive
`sudo dd if=<<image-file>>.img of=/dev/<<usb-drive>>`
