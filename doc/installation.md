# Installing Carnap

This guide will provide instructors for getting started with Carnap
development: installing and building a local copy of the software that you can
tinker with on your own machine. This is a useful thing to be able to do if you
want to contribute changes and bugfixes to the project, or if you eventually
want to deploy your own instance Carnap.

<!-- TODO: Link to deployment guide -->

## Requirements

Carnap has two components: `Carnap-Client` contains the code to
display and check exercises. `Carnap-Server` contains the code for the
Carnap web application (administering courses, uploading exercises,
submitting solutions, etc.). Both have to be built and installed for
Carnap to work.

To install Carnap you need:
- A computer to build and run Carnap on. Currently Linux and MacOS are
  supported, but it is possible to build and run Carnap on Windows
  using the [Windows Subsystem for
  Linux](https://docs.microsoft.com/en-ca/windows/wsl/).
- The source code for Carnap from
  [GitHub](https://github.com/Carnap/Carnap).
- Software to build Carnap.

Warning: building Carnap requires a large amount of memory (about
12GB) to compile. You should probably close all other applications and
background services (Zoom, Slack, etc.) when doing it.

## Building Carnap

### Installing Nix

The easiest way to build Carnap is using the Nix package manager.
Carnap comes with information Nix uses to build Carnap and all its
dependencies automatically, without you having to install anything
else by hand.  The build using Nix will use self-contained tools to
reduce the risk of incompatibilities between, e.g., a Haskell compiler
you have installed and what Carnap requires. 

To install Nix, follow the [Installation
instructions](https://nixos.org/manual/nix/stable/#chap-installation)
for your platform.  On Linux, this just requires the command
```
$ sh <(curl -L https://nixos.org/nix/install)
```
from the terminal command line as a user who has `sudo` access.

(The `$` indicates the command line prompt, you only enter the
commands to the right of it.)

If you want to compile using nix on a machine where you don't have `sudo`
access, some alternative nix installation approaches are described in the
[nixos wiki](https://nixos.wiki/wiki/Nix_Installation_Guide). In particular a
`nix-user-chroot` installation has been confirmed to work for compiling Carnap.

You can significantly speed up builds by using binaries for Carnap
dependencies from Carnap's [Cachix](https://cachix.org/) instance,
which has support for both Linux and macOS. To use it, say:
```
$ nix-env -iA cachix -f https://cachix.org/api/v1/install
$ cachix use carnap
```

### Download the Source Code

The latest version of Carnap's source code is available in the [GitHub
repository](https://github.com/Carnap/Carnap). Click on the "Code"
button. If you have `git` installed and configured for ssh access,
this command should do the trick:
```
$ git clone git@github.com:Carnap/Carnap.git
```
This downloads the source code into the directory `Carnap`. Change to
that directory by saying
```
$ cd Carnap
```

### Run the Development Server

Once you're in the `Carnap` directory, you can use `nix` to build the different
components of the system. Some useful recipes for building in different ways
have been recorded in Carnap's included Makefile. If you're interested in
building a simple development server (which doesn't require any extra database
or authentication configuration) then you can simply issue the command
```
make devel
```
This will build Carnap's client-side component (the JavaScript proof-checker
that runs in the browser), and will then build and activate a Carnap server. By
default, you'll be able to reach this server by navigating to
`http://localhost:3000` on the computer where the server is running. Warning:
as noted above, the initial build may take some time, and may require a lot of
memory.

Issuing `make devel` again after the initial build will reactivate the server,
unless you've made any changes to your copy of Carnap source code. If you have
made changes, then reissuing `make devel` will rebuild any parts of the client
and server that are downstream from your changes, and will then reactivate the
server. Some behavior of the development server (like whether the server
appears at http://localhost:3000, or somewhere else) can be controlled by
changing environment variables. For details, see the 
[server configuration documentation](./server-config.md)

## Server Setup

Once your server is configured and running, you have to provide yourself with
an administrator account if you want to create any instructors.

Go to your newly minted Carnap instance and log in - because you're running in
development mode, you can log in as whatever you'd like by just typing in an
identifier. Then go to `http://localhost:3000/admin_promote` (or to the
corresponding address if you've edited the settings file so that you're serving
on something other than `localhost:3000`) and click the button. You will now be
the administrator of this instance. Multiple administrators are supported, but
there is not yet a user interface to enable this.

You can now administrate your server (including promoting instructors, and
configuring LTI platforms) at `http://localhost:3000/master_admin`

## Carnap's user documentation

> Does this section belong in server configuration?

The data directory (by default, `Carnap/dataroot`) can also contain a
subdirectory `srv`, whose contents are directly available at `/srv/` on the
Carnap instance. This is used for documentation on the production instance at
`carnap.io`. The menu for Carnap instructors contains a link "Documentation"
which points to `/srv/doc/index.md`.

If you want site-specific documentation, you should create the
directory `srv/doc/` inside your data directory, and place a MarkDown
file `index.md` there as the starting point.  If you want to provide
Carnap's official documentation on your Carnap instance, you can
download it into said directory:
```
$ cd dataroot
$ git clone git@github.com:Carnap/Carnap-Documentation.git srv
```
