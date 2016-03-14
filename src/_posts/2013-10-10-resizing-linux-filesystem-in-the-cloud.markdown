---
layout: post
title: "Resizing Linux disk drives in the cloud"
date: 2013-10-10 22:43
comments: true
categories:
published: true
---

Recently, we had a few AWS instances fill up disk space.  The problem manifested itself
in javascript errors and images not display correctly to users of our web application.
There were a few ways we could have went about correcting it (we tried 2).

First, we walked through Amazon's process of resizing a disk and discovered the process
to be too painful because of the downtime it required to our instances.  After looking
at our filesystem growth and application set up, we then decided it was worth our time
to add a 2nd ebs storage object for the extra storage. Our setup allowed for us to do
this easily because all application level data was stored under a root directory
we use for application code, data, and logs.

In addition to relieving pressure on the disks, it also afforded us the opportunity
to use different disk profiles in case we wanted different IOPS profiles.
This could prove valuable if we wanted to utilize this method on our database servers
in the future.

Here is the overview of steps we performed (pardon the messiness until I redocument)

1. Create an ebs store in Amazon
2. Attach it to the running instance.  This should mount the device in the /dev folder
```
/dev/sdf through /dev/sdp
Note: Newer linux kernels may rename your devices to /dev/xvdf
through /dev/xvdp internally, even when the device name entered
here (and shown in the details) is /dev/sdf through /dev/sdp.
```
3. Identify the device added with
```
    fstab
```
4. Make the filesystem (Format it)
```
sudo mkfs -t ext3 device_name
> mke2fs 1.40.4 (31-Dec-2007)
> /dev/sdh is entire device, not just one partition!
> Proceed anyway? (y,n) y
```
5. Create a mount point for the filesystem
```
# mkdir /mnt/myvolume
# mount /dev/sdh /mnt/myvolume
```
6. Check that it is mounted with 'df' and then just 'cd' to it and start using the space.
7. Perform a copy to move old files to new files using [CPIO](http://www.thegeekstuff.com/2010/08/cpio-utility/)

### References used

[1](http://embraceubuntu.com/2006/01/29/move-home-to-its-own-partition/)
