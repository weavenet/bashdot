[![CircleCI](https://circleci.com/gh/weavenet/bashdot/tree/master.svg?style=svg)](https://circleci.com/gh/weavenet/bashdot/tree/master)

# Summary

I am **bashdot**.

I am a minimalist dotfile management framework focused on supporting multiple
profiles, providing different configurations based on the profiles installed
on a given system.

I am written **100% in bash**, require **no dependencies** outside of bash, and am [tested](https://circleci.com/gh/weavenet/bashdot/tree/master) using [bats](https://github.com/sstephenson/bats).

## Overview

Bashdot works by symlinking all files and directions in **profiles**, within the current
directory where bashdot is run, to files in the users home.

One or more profiles can be installed on a specific computer to provide
the desired dotfiles for it's purpose (work, home, shared, public, etc.).

## Quick Start

To setup your own bashdot managed dotfiles:

* Fork this repo to your account
* Clone down your fork of the repo (you can clone into Dropbox or Google Drive to sync
across multiple systems) 
* Run the following to setup the dotfiles for the **public** profiles on this instance.

```
bash bashdot install public
```

## Managing Multiple Profiles

Bashdot works by symlinking files within the given profile directory into your home directory.

For example, if you run:

```
bash bashdot install public private
```

Bashdot will symlink all the files in the public and private directories within profiles
into your home directory while prepending a "period".

The above command would create the following symlinks:

```
lrwxrwxrwx 1 brett brett   28 Mar  8 09:03 .bashrc -> /brett/bashdot/profiles/public/bashrc
lrwxrwxrwx 1 brett brett   40 Mar  8 09:03 .profilerc_private -> /brett/bashdot/profiles/private/profilerc_private
lrwxrwxrwx 1 brett brett   38 Mar  8 09:03 .profilerc_public -> /brett/bashdot/profiles/public/profilerc_public
```

You can then make changes to files in the **public** or **private** profiles, or
add additional profiles as necessary.  If you use different files in different
environments you can create a profile for each environment with the appropriate dotfiles.

Since the files are symlinked from home, if you keep the files in a shared
drive, changes to files on one instance will automatically be reflected on all
instances with that profile installed.

The default **.bashrc** will load anything in file prepended with **profilerc** to
allow for doing any specific setup for the a profile. See
[profiles](https://github.com/weavenet/bashdot/tree/master/profiles)
for examples of profiles with different variables initialized.

## Frequently Asked Questions

**Q:** Does bashdot support templates or user input for configuring dotfiles during installation?

**A:** No, if you have different configurations of a single dotfile, bashdot handles that
by supporting multiple profiles. For example if you want to setup differnet **.gitconfig**
for your **home** and **work** environments, create a home and work profile, and within each of
those profiles add the appropriate gitconfig, then use bashdot to install the approriate profile
on each system.

**Q:** What if I have secrets or other private information to install in my dotfile?

**A:** Never check in sensitive information in your dotfiles. To remove sensitive information,
either a) pull that information from an external system or b) encrypt it and read the decryption
key from a location not in your dotfiles. See [here](https://gist.github.com/weavenet/f3af28350f07176674a5474b2d891102) for examples.

## Bashdot Development

### Test

Only requirement to run tests is [docker](https://docs.docker.com/install/). Once installed run:

```
make test
```
