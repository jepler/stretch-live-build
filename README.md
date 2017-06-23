# stretch-live-build
Scripts supporting the build of the linuxcnc stretch live cd image

When run on a Debian Stretch amd64 system, this produces an approximately 2GB image that can be booted via USB.
It includes the 64-bit "preempt-rt" kernel, the latest linuxcnc 2.7.x "uspace" release, and uses the xfce desktop.

It requires the `live-wrapper` package, and assumes that there is a HTTP proxy at http://localhost:8001/
(I use squid-deb-proxy, which defaults to 8000, so install it and change the default;
other proxy choices such as apt-cacher, apt-cacher-ng, and apt-proxy appear to be incompatible with `live-wrapper`)

## Current status
This has been tested by nobody but me.  It will probably let your chickes out of the coop, make your goats' milk sour, etc.
Not to mention ruining machine tools galore.

The usual set of "non-free" firmware is included, but I didn't test any firmware that requires it.
Because the non-free firmware is included, I expect the image to have generally the same wireless support as Debian Stretch.

## Items I tested:
* Boots in qemu when used as a "cdrom" installation image
* installs into a 20GB virtual hard drive, using "one filesystem" partitioning.  Installed system has rt kernel and linuxcnc package
* Boots off a 32GB USB stick (copy with 'dd')

## Important notes
* The live user's name/password is user/live.  Use this if the screen locker activates.
* When installing, enter blank for the root password (twice) so that the initial user can use 'sudo' to become root

## Known limitations
* Actual installation requires a network at install time
* The installation is a "frankendistro", combining some packages intended for Debian Jessie
  (this can be changed as soon as 2.7.10 is released with packages for stretch)
* On most systems, the "preempt-rt" kernel is not suitable for software step generation
* on a 20GB virtual hard drive, the "separate partitions" method failed, I think because the disk filled
