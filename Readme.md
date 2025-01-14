reMarkable 2 Docker image
=========================

This repo contains a docker file for building a container containing an emulator
for the remarkable 2 OS.

Usage
-----

```
> docker build -t rm-docker .
> docker run --rm -v rm-data:/opt/root -p 2222:22 -it rm-docker
# Lots of boot messages...
Codex Linux 3.1.266-2 reMarkable ttymxc0

reMarkable login:

# Now login using the root account, no password
# Or ssh:
ssh root@localhost -p 2222
```

Targets
-------

### qemu-base

Use `docker build --target qemu-base` to build a basic qemu image.

### qemu-toltec

The `qemu-toltec` target will install [toltec](https://toltec-dev.org/) in
the image.

### qemu-rm2fb

The `qemu-rm2fb` target (which is the default) will include a framebuffer
emulator from [rm2-stuff](https://github.com/timower/rM2-stuff/tree/dev).

X11 forwarding can be used to view the framebuffer:
```
docker run --rm \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  -v $HOME/.Xauthority:/root/.Xauthority \
  --env DISPLAY \
  -h $(hostnamectl hostname) \
  -p 2222:22 \
  -it rm-docker:plain
```

References
----------

Largely based on https://gist.github.com/matteodelabre/92599920b46e5fac9daf58670d367950
