# run-pihole

Run pihole in a docker container

See this: https://github.com/pi-hole/docker-pi-hole

Clone this repo and run `./pihole` as explained below:

Works on Linux and on MacOS.

In its simplest form, just run:

```
./pihole
```

The script attempts to glean the existing DNS configuration and to
configure the container to use those servers as its upstream
resolvers.

If that won't work, just pass the explicit servers as arguments
on the command line.

For examplem to set up pihole to hit Cloudflare's servers, do this:

```
./pihole 1.1.1.1
```

## PiHole configuration (additional block lists, etc.)

The `./lists` script here sets up the pihole configuration as
explained in this blog post:
https://hobo.house/2018/02/27/block-advertising-with-pi-hole-and-raspberry-pi/

The `pihole` shell script waits for the container to be operational and then
it runs the configuration script. Configuration data persists in the `./config/`
directory.

By default, this script is set up to use the Quad9 DNS servers.

Once the pihole container is up, set up your laptop's DNS to
use 127.0.0.1 as its DNS.

## Set up MacOS DNS settings via commandline

From http://osxdaily.com/2015/06/02/change-dns-command-line-mac-os-x/

To set up the DNS on MacOS, you can do:

```
networksetup -setdnsservers Wi-Fi 127.0.0.1
```

To reset it (when you are no longer using it):

```
networksetup -setdnsservers Wi-Fi Empty
```

If you are using a different network adapter, you may have to replace
the `Wi-Fi` above with whatever the appropriate service name is, gleaned by
running `networksetup -listallnetworkservices`

## Stopping pihole, upgrading, etc.

To stop the container, you can use `docker stop pihole`

To restart the container, `docker start pihole`

To destroy it entirely, `docker rm -f pihole`

Upgrade by doing a `docker pull`:

```
docker rm -f pihole
docker pull pihole/pihole
./pihole
```

## Convenient aliases

After the `pihole` script runs, it outputs a message like this:

```
Source the /home/yourlogin/src/run-pihole/aliases.bash file for some useful aliases.

. /home/yourlogin/src/run-pihole/aliases.bash
```

#### start-pihole

Starts the pihole container and sets the local DNS to 127.0.0.1

#### stop-pihole

Stops pihole and resets DNS to defaults.

#### purge-pihole

Stop pihole and remove the contents of the `config/` directory, so pihole
will recreate it on startup.

#### set-dns-local

Set the DNS to 127.0.0.1

#### set-dns-empty

Reset DNS setting to defaults.

#### get-dns-server

Show the current list of DNS servers.
