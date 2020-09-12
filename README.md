# ddclient (snap)

ddclient is a Perl client used to update dynamic DNS entries for accounts on many dynamic DNS services.

See supported services in the offical [read me](https://github.com/ddclient/ddclient#ddclient-v391) of ddlient's repository at github.

[![Get it from the Snap Store](https://snapcraft.io/static/images/badges/en/snap-store-black.svg)](https://snapcraft.io/ddclient-snap)
[![Donate with PayPal](https://giaever.online/paypal-donate-button.png)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=69NA8SXXFBDBN&source=https://git.giaever.org/joachimmg/ddclient-snap)

## Usage

When this snap is installed, there will be a background daemon running (called `ddclient-snap.daemon`). This daemon reads your configuration from the file `/var/snap/ddclient-snap/current/etc/ddclient/ddclient.conf`.

Fill in your details and restart the service with `snap restart ddclient-snap.daemon`. If you're having problems, please see the [question asked by a user](https://git.giaever.org/joachimmg/ddclient-snap/issues/1).

If you want to execute commands manually, you'll have the exectuable available with `ddclient-snap.exec`.

## Build and installation instructions

### Install from The Snap Store (Recommended)

Make sure you have Snapd installed on your system. See [Installing snapd](https://snapcraft.io/docs/installing-snapd) for a list of distributions with and without snap pre-installed, including installation instructions for those that have not.

```bash
$ snap install ddclient-snap
```

### Build this snap from source

We recommend that your download a pre-built version of this snap from [The Snap Store](https://snapcraft.io/ddclient-snap), or at least make sure that you checkout the latest tag, as the master tag might contain faulty code during development.

1. **Clone this repo and checkout the latest tag**

```bash
$ git clone https://git.giaever.org/joachimmg/ddclient-snap.git

# Go into directory
$ cd ./ddclient-snap

# Checkout tag
$ git checkout <tag>
```
_**NOTE**: You can find the latest tag with `git ls-remote --tags origin`_

2. **Build and install**

Make sure you have snapd (see [Installing snapd](https://snapcraft.io/docs/installing-snapd)) and latest version of Snapcraft. Install Snapcraft with

```bash
$ sudo snap install snapcraft --classic
```

Or update with

```bash
$ sudo snap refresh snapcraft
```

2.2 **With multipass**

From the «ddclient-snap»-directory, run

```bash
$ snapcraft
```

Multipass will be installed and a virtual machine will boot up and build your snap. The final snap will be located in the same directory.

2.3 **With LXD** (*required* for Raspberry Pie)

Snapcraft will try to install multiplass and build the snap for you, but on *Raspberry Pi* it will fail. You will have to use an LXD container.

Install LXD and create a container

```bash
$ snap install lxd
$ snap lxd init
```

Make sure your user is a member of lxd-group

```bash
$ sudo adduser $USER lxd
```

Launch an Ubuntu 20.04 container instance

```bash
$ lxc launch ubuntu:20.04 ddclient-snap
```

**Clone repo as described in #1**

Make sure you're in the «ddclient-snap»-directory and go into the shell of your newly created container

```bash
$ lxc exec -- ddclient-snap /bin/bash
```

and run

```bash
$ SNAPCRAFT_BUILD_ENVIRONMENT=host snapcraft
```

when the build is complete, you'll have to exit the shell and pull the snap-file from the container. See `lxc file pull --help`.

3. **Install new built snap**

```
$ sudo snap install ./ddclient-snap_<source-tag>.snap --dangerous
```
