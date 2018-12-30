# run-pihole

Run pihole in a docker container

See this: https://github.com/pi-hole/docker-pi-hole

Clone this repo and run `./pihole` as explained below:

Works on Linux and on MacOS.

In its simplest form, just run:

```
./pihole
```

This will wait 30 seconds for the container to come up, then run the
`./lists` script to set up the pihole config as explained in this blog
post: https://hobo.house/2018/02/27/block-advertising-with-pi-hole-and-raspberry-pi/

If 30 seconds is not enough time, then run it like this:

```
./pihole 60
```

By default, this script sets up the pihole container to use the Quad9 DNS servers.
If that won't work (or you need to run the container in a corporate network),
just set the DNS servers in the `PIHOLE_DNS` environment variable.

```
PIHOLE_DNS="1.1.1.1" ./pihole 60
```

The above will set up pihole to hit Cloudflare's servers and set up the extra
lists after waiting 60 seconds.

Once the pihole container is up, set up your laptop's DNS to use 127.0.0.1
as its DNS.

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
