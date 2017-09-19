This is a docker image to allow you the ability to run the
Unifi Video Controller on a Synology NAS.  The image requires
you to run the container with a number of extra capabilities, as 
well as disabling apparmor for the container and mounting a host
volume to store all your configuration, videos, and mongodb database
files into the /var/lib/unifi-video location on the container.

The Synology Docker UI doesn't provide the ability to set these
more esoteric security policies, so if you want to start it from there
you will need to select "privileged" mode for the container.

Alternately, if you prefer to have a more reduced security
profile you can run it from the command line.  Here's an example
from my system, you may need to change the directory for
the host volume mount:

```
docker pull supafyn/unifi-video-controller:latest

docker stop unifi-video

docker rm -f unifi-video

docker run -d --restart=always --name=unifi-video -h unifi-video --net=host -p 1935:1935 -p 6666:6666 -p 7080:7080 -p 7442:7442 -p 7443:7443 -p 7445:7445 -p 7446:7446 -p 7447:7447 -d -v /volume1/docker/unifi-video:/var/lib/unifi-video --cap-add=SYS_ADMIN --cap-add=DAC_READ_SEARCH --cap-add=NET_BIND_SERVICE --cap-add=SYS_PTRACE --cap-add=SETUID --cap-add=SETGID --security-opt apparmor:unconfined supafyn/unifi-video-controller:latest
```
