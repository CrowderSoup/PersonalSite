+++
title = "Build a Torrent Machine and Network Share"
date = "2016-01-21 13:00:00"
categories = ["Raspberry Pi"]
tags = [
    "raspberry pi",
    "torrent",
    "projects"
]
+++

When I first got a Raspberry Pi the first thing I wanted to build was a home
server. I wanted to have a central place at home to store files. I also thought
it would be nice to have a torrent machine to handle downloading whatever I
wanted. This past weekend I was finally able to get around to building it with
a Raspberry Pi 2.

I chose to use [Diet Pi](1) as my OS. Diet Pi is an OS that comes with only the
bare essentials installed. On first boot it gives you a list of preconfigured
software to install. This was perfect for me because I could install Samba for
my file server and transmission for torrents. It made setting up what I wanted
**really** easy.

The process *actually* was **really** simple. So this blog post won't need to
go into heavy technical detail. Instead, I just want to walk through the simple
process of steps, with a couple of images, to document it for myself. Hopefully
others benefit from this as well!

First I downloaded the [Diet Pi image](2) (based on Debian Jesse) and unziped it.
Then I made sure my SD card was clean and ready to flash. I like to use the
Windows CLI tool `diskpart`. You can see pretty simply the steps I took from the
image below:

![Cleaning my SD Card]({{< baseurl >}}assets/uploads/2016/01/clean_disk_windows_powershell.png)

Once my SD Card was clean, I formatted it:

![Formatting my SD Card]({{< baseurl >}}assets/uploads/2016/01/new_simple_volume_disk_management.png)

It doesn't matter what format you use because you're going to reformat it when
you write the image to the SD card (I use [Win32DiskImager](3)):

![Write Image to SD Card]({{< baseurl >}}assets/uploads/2016/01/write_img.png)

### Notes

- Install DietPi
- Install relevant software thought dietpi installer
- Configure softwares


[1]: http://dietpi.com/
[2]: http://goo.gl/EsIvUp
[3]: http://sourceforge.net/projects/win32diskimager/
