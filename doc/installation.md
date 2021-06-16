# Installing Carnap

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

### Download the source Code

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

### Build the Carnap components

To build the Carnap client, say
```
$ nix-build -j4 -A client -o client-out
```
> Is the `-j4` necessary/useful?

This should produce a directory `client-out` containing the compiled
Carnap-Client components.

To build the Carnap server, say
```
$ nix-build -j4 -A server -o server-out
```

### Running the Carnap server

> Would be nice to set it up so that this is it if you just want a
> sandbox with `sqlite`, no Google authentication, defaulting to
> `Carnap/dataroot` to store the data, this is all you have to do. Maybe
> provide a script `run-carnap` that you can then invoke that just does
> `cd Carnap-Server; ../server-out/bin/Carnap-Server` and you can go to
> `localhost:3000` and it's all there. As it is we have to do the following,
> and since this builds a production server with Google
> authentication, you won't be able to log in!

Now run the Carnap server using
```
$ mkdir dataroot; cd Carnap-Server; ../server-out/bin/Carnap-Server
```
and point your browser to http://localhost:3000. You should see the
Carnap front page.

## Configuring Carnap

Carnap uses a settings file, `settings.yml`, to store its
configuration. You can find the example version at
[`Carnap-Server/config/settings-example.yml`](https://github.com/Carnap/Carnap/blob/master/Carnap-Server/config/settings-example.yml).
To utilize binary caching, Nix builds Carnap using this example
configuration file, and users are expected to use environment
variables or provide a different settings file at runtime. You do this
by passing the name of the settings file as the first argument to the
`Carnap-Server` executable. Also, all settings are configurable by
environment variables, which is useful for Docker deployments. For
instance, you can copy `Carnap-Server/config/settings-example.yml` to
`mysettings.yml`, make changes, then start the server using
```
$ server-out/bin/Carnap-Server mysettings.yml
```
The settings file lets you set a number of variables, the most
important of which are:

Name | Purpose
-----|--------
STATIC_DIR | The location of the `static` directory where Carnap looks for things like CSS style sheets, script files, and fonts.
APPROOT | The address at which the Carnap server will be accessed.
DATAROOT | The location of Carnap's data directory.
BOOKROOT | The location of the directory holding the Carnap book.
GOOGLEKEY | The API key for Google authentication
GOOGLESECRET | The Google Auth secret string
--------------

### Directories

The Carnap server needs access to three directories. These are:

- The data directory, which holds uploaded documents,the cookie
  encryption key, and the database containing user, course, and
  submission data (if Carnap uses `sqlite` to administer the database,
  and not a database server).  It must be writable by the Carnap
  server process, and its location is given as the `DATAROOT`
  variable. This can be anywhere you like, but the build environments
  have it in `Carnap/dataroot`. The directory must exist when you run
  the server.
- The directory holding static files such as CSS style sheets and
  JavaScript files. Its location is given as the `STATICROOT`
  variable. In the source distribution, this directory is located in
  `Carnap/Carnap-Server/static`.(If you want Carnap to locate these
  files somewhere else you can instead set the `STATICROOT` variable
  to the full URL of the static directory.)
- The book directory holds the Carnap book. In the source
  distribution, this directory is located in `Carnap/Carnap-Book`.

Paths to these directories should be absolute, or relative to the
directory from which you run the Carnap server.  For instance, if you
want to run Carnap from the source directory, your `mysettings.yml`
file should contain the following lines:
```
static-dir: "_env:STATIC_DIR:Carnap-Server/static"
data-root: "_env:DATAROOT:dataroot"
book-root: "_env:BOOKROOT:Carnap-Book"
```

### HTTP access

Carnap is obviously a web application, and the Carnap server needs to
know where you (or your users) will access it.  The two relevant
variables are `APPROOT`, which is the URL of the Carnap server, and
`PORT`, which is the TCP port where Carnap will be provided on the
local machine.

For testing purposes, it is often enough to provide the Carnap app
locally on your machine only, and not make it accessible from the
network.  In such a situation, your `mysettings.yml` file should
contain the lines:
```
port: "_env:PORT:3000"
approot: "_env:APPROOT:http://localhost:3000"
```
This will make Carnap available on your machine only at the URL
http://localhost:3000.

If you are making Carnap available over the network, you need to know
the URL at which Carnap will be available, and set a reverse proxy on
the server with that address to the host/port where Carnap is hosted.
For instance, say you want Carnap to be accessible at
`https://carnap.bigstateu.edu`, and Carnap runs on the server
`webappserv.bigstateu.edu` on port 3000. Then your web administrator
has to set a reverse proxy that translates HTTP requests for
`https://carnap.bigstateu.edu` internally to
`webappserv.bigstateu.edu:3000`. Your `mysettings.yml` file should
then contain the lines:
```
port: "_env:PORT:3000"
approot: "_env:APPROOT:https://carnap.bigstateu.edu"
```

If your machine is accessible from the internet and you want to make
your own Carnap server available, you could use a simple solution such
as [caddy](https://caddyserver.com/docs/quick-starts/reverse-proxy).

### Database

If the setting variable `SQLITE` in settings.yml is set to true (default), or
if the environment variable SQLITE is set to true, Carnap will generate
a lightweight database for storing its data, using ([SQLite](https://www.sqlite.org/)).

If SQLITE is set to false, Carnap will instead use a PostgreSQL database. Set
the environment variable `SQLITE=false` and supply `PGUSER`, `PGPASS`,
`PGHOST`, and if required, `PGPORT` and `PGDATABASE` for your postgresql
database instance.

Which database should you use? Sqlite is simpler to manage, and should be
adequate for most installations with fewer than 500 users. For larger
installations, PostgreSQL may be appropriate.[^1]

[^1]: Why? PostgreSQL is preferred in industry, and may have some security
advantages depending on your server configuration. Sqlite also doesn't have the
same level of support for concurrent writes to the database as PostgreSQL, but
Carnap retries database transations that fail becuase the database is busy, so
this shouldn't generally cause any trouble in low-traffic scenarios.

If you wish to use peer authentication via Unix socket on a locally hosted
PostgreSQL database, set all of `PGUSER`, `PGPASS`, `PGHOST` and `PGPORT` to
empty strings.

## Authentication

Carnap servers currently require Google authentication to be
configured for administration purposes, even if it is not intended to
be used by students. (See the [LTI 1.3 documentation](lti.md) for
details on how to configure LTI authentication, after [completing
setup](#server-setup)).

> Is there a way to run Carnap without Google Auth once it's built
> without the `dev` flag?  If not, how do you build it without Google
> Auth if you really just want to play on your laptop?

Setting up Google authentication requires setting up a Google APIs project.

First, create a project in [Google's developer
console](https://console.developers.google.com/cloud-resource-manager).
Then, create an OAuth2 client ID under [Google
credentials](https://console.developers.google.com/apis/credentials).

It will show up like this:

![image of the client ID page](./images/google-creds.png)

Click "Create Credentials". On the client ID page, set an Authorized
Redirect URI for `APPROOT/auth/page/google/callback`, where `APPROOT`
should be replaced by the value of your `APPROOT` settings variable.

![image of the authorized redirect URIs page](./images/google-client-id.png)

> The following didn't make sense to me and I don't recall seeing
> anything about scopes.

On your OAuth2 Consent Screen tab, no scopes need to be added as Carnap just
needs emails to log in.

Once you've configured all the information on the Google side, fill it in the
Carnap settings file:
```
google-api-key: "_env:GOOGLEKEY:<your Google client ID>"
google-secret: "_env:GOOGLESECRET:<your Google secret>"
```

## Server Setup

Once your server is configured and running, you have to provide
yourself with an administrator account. 

Go to your newly minted Carnap instance and log in with Google. Then,
go to `APPROOT/admin_promote` (where `APPROOT` again is the URL of
your Carnap server, e.g., http://localhost:3000/admin_promote) and
click the button. You will now be the administrator of this instance.
Multiple administrators are supported, but there is not yet a user
interface to enable this.

You can manage the site including promoting instructors, managing
students, and configuring LTI platforms at
`APPROOT/master_admin` (e.g., http://localhost:3000/master_admin)

## Carnap's user documentation

The data directory (`DATAROOT`) can also contain a subdirectory `srv`,
whose contents are directly available at `/srv/` on the Carnap
instance. This is used for documentation on the production instance at
`carnap.io`. The menu for Carnap instructors contains a link
"Documentation" which points to `/srv/doc/index.md`.

If you want site-specific documentation, you should create the
directory `srv/doc/` inside your data directory, and place a MarkDown
file `index.md` there as the starting point.  If you want to provide
Carnap's official documentation on your Carnap instance, you can
download it into said directory:
```
$ cd dataroot
$ git clone git@github.com:Carnap/Carnap-Documentation.git srv
```
