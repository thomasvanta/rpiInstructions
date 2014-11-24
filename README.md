# Instructions

## Prerequisites

1. Install [VirtualBox](https://www.virtualbox.org/).
1. Install [vagrant](http://www.vagrantup.com/).
1. Install [Ansible](http://ansible.com).  I used [pip](https://devopsu.com/guides/ansible-mac-osx.html).
    2. Install Xcode
    2. sudo easy_install pip
    2. sudo pip install ansible --quiet
    2. Then, if you would like to update Ansible later, just do:
    2. sudo pip install ansible --upgrade


## Other Dependencies

1. Clone this repository and cd into it.
1. Download your preferred Raspberry Pi SD card image.  I'm using [2014-09-09-wheezy-raspbian](http://downloads.raspberrypi.org/raspbian_latest).  Unzip it, and symlink it with `ln -s 2014-09-09-wheezy-raspbian.img image.img`
1. Download a zip file of the Raspberry Pi [cross-compiler tools](https://github.com/raspberrypi/tools/archive/master.zip).  Make sure the zip file is named `tools-master.zip`.  Leave it compressed.
1. Download [OpenFrameworks for armv6](http://www.openframeworks.cc/versions/v0.8.4/of_v0.8.4_linuxarmv6l_release.tar.gz).  Leave it compressed.

## Get the image ready
_You only have to do this if you're not using 2014-09-09-wheezy-raspbian._

The NFS root with which you're booting the Pi lives in the image.img file.  You need to calculate the offsets to the boot and root partitions on that device.  On OSX you can just type `file image.img`.  The relevant information here is the start sector for the boot (1st) and root (2nd) partitions.  Multiply the start sector by the block size (512) to get the byte offset.  Put these numbers in `offset_boot` and `offset_root` in playbook.yml.

## Create the virtual machine

1. Configure a _wired ethernet_ network.  I use a USB Ethernet adapter on my Macbook.  Set the IP/netmask of the wired connection to `10.0.0.2/255.0.0.0`.  The IP address of the virtual machine is hard-coded to `10.0.0.1`.
1. Type `vagrant up`.  It will probably ask you to select the network interface to bridge to.  Select your wired connection.
1. The machine will start and provision itself.  If there's an error and the provisioning doesn't complete, you can type `vagrant provision` to retry the provisioning process.
1. Get a cup of coffee.  It'll take awhile.
1. Type `vagrant ssh` to connect to and begin using your new environment.




## Vagrant commands and [tutorial](https://docs.vagrantup.com/v2/getting-started/index.html)

1. vagrant up
1. vagrant ssh
1. vagrant suspend
1. vagrant halt
1. vagrant destroy
