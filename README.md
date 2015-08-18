freetz-vagrant
==============

Set up a build environment for [Freetz](http://freetz.org/), a firmware-extension (modification) for
the AVM Fritz!Box, using [Vagrant](http://www.vagrantup.com/) and
[Ansible](http://www.ansible.com/).

Usage
==============

Install necessary software
--

1. Install VirtualBox from http://www.vagrantup.com/
2. Install Vagrant from http://www.vagrantup.com/
3. Install Ansible from http://www.ansible.com/

Note: you can use Vagrant with other desktop virtualization software, see
  the Vagrant documentation for detail.

Bring up the virtual machine
--

1. Clone this repo
2. Edit Vagrantfile to adjust the Subversion URL (stable or trunk)
3. If you have a Freetz `.config`, place it in the top-level directory
(alongside the `Vagrantfile`) as `config`.
4. Provision the VM with `vagrant up`. Depending on the speed of your
internet connection, this will take between 5 and 30 minutes, and will
download about 500 MB for the image, and about 150 MB for the necessary
packages.
5. Enter the VM with `vagrant ssh`
6. Run the Freetz build

```bash
cd freetz
make menuconfig
make
```

Running `make` will download all necessary tools, the selected original AVM
firmware that will be modified, the package sources, etc., and
build the packages.  Depending on the speed of your internet connection and
your computer, this will take about 30 minutes and download about 100 MB.

If everything works, the `make` command should output something like:

```
STEP 3: PACK
  checking for left over Subversion directories
  integrate freetz info file into image
packing var.tar
creating filesystem image
  SquashFS block size: 64 kB (65536 bytes)
merging kernel image
  kernel image size: 13.4 MB, max 15.4 MB, free 2.0 MB (2104832 bytes)
  Aproximately maximal time for the answering machine: 14 min, 41 sec (881 sec)
packing images/7240_06.05-freetz-devel-13365.de_20150818-143843.image
  image file size: 14.4 MB
done.

FINISHED

real	9m31.012s
user	7m53.560s
sys	1m2.584s
```


Saving the image and configuration
--

The final firmware image is available in the `images` directory (in
`~/freetz/images` inside the VM, and `./images` on the host).

The Freetz configuration file `.config` is stored in the top level
directory as `config`.  When you ssh into the VM, a symlink is automatically
created at `~/freetz/.config`.  Running `menuconfig` will replace this
symlink with the new configuration file.  When you log out, that file will
automatically be copied back.


Cleaning up
--

After the image has been built, you can destroy the VM:

```bash
vagrant destroy
```

This will remove the VM including it's virtual hard disk, and all downloaded
files.
