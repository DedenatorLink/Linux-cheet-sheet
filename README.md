# Linux cheet sheet
---

## General

► Command for every line in document

    while read in; do [COMMAND] $in; done < [DOCUMENT]  

► cls command

    clear ; printf '\033[3J'

► hash

|sha256     |md5sum  |
|-----------|--------|
|`sha256sum`|`md5sum`|
    

► Mount iso

    sudo losetup -P /dev/loop0 iso.iso 

► List images (documents with extension `png` or `jpg`)

    ls {*.png,*.jpg}

► Project screen (extend)

    xrandr --output eDP-1 --left-of HDMI-1

## Admin

► Partition structure on disk

    sudo sfdisk -d 

► Create false USB (partition)

    fallocate -l 2G usb.iso

► Format iso to linux partition

    mkfs -t ext4 usb.iso

► Download package with dependencies

    apt-cache depends -i [PACKAGE] | awk '/Depends:/ {print $2}' | xargs  apt-get download && apt-get download [PACKAGE]

## Media

► Pdf to images
* Convert

    `convert -density 300 pdf.pdf img.png`

* pdfimage (*-j for jpg, -png for png*)

    `pdfimages pdf.pdf folder/prefix`

► Better image to pdf conversion

    convert -density 72 *.jpg pdf.pdf

► Standard image format rename

    exiftool '-FileName<CreateDate' -d IMG_%Y%m%d_%H%M%S%%-c.%%e .

► Download youtube video in 720p without sponsors

    yt-dlp --sponsorblock-remove sponsor -f 22 [PLAYLIST_LINK]


► Download youtube video playlist in 720p without indexes

    youtube-dl -o "%(playlist_index)s-%(title)s.%(ext)s" [PLAYLIST_LINK]

► Remove exif data

    exiftool -all= *

► Find *'pattern'* in documents located in */path/to/somewhere/* 

    grep -rn '/path/to/somewhere/' -e 'pattern'

► Random rename

    for old in *; do new=`xxd -l 16 -ps /dev/urandom`; while [ -f "$new" ]; do new=`xxd -l 16 -ps /dev/urandom`; done;  ext="${old##*.}"; mv "$old" "$new.$ext" ; done ;

## rename

► Rename files to first `10` characters + extension (-n for preview)

    rename 's/^(.{10}).*(\..*)$/$1$2/' *

► Remove first `10` characters from name

    rename 's/.{10}(.*)//' *

► Rename file to last `10` characters

    rename 's/.*(.{10})(\..*)$/$1$2/' *

► Rename file to first and last `10` characters

    rename -n 's/^(.{10}).*(.{10}\..*)$/$1$2/' *

► Add prefiks to file

    rename 's/^/PREFIX_/' *

## First boot

► Fix windows linux dual boot clock problem

    timedatectl set-local-rtc 1 --adjust-system-clock

► Remove grid from Cinnimon desktop 

    gsettings set org.nemo.desktop use-desktop-grid false

---
