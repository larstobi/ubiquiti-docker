This is a docker image to allow you the ability to run the
Unifi Controller on a Synology NAS.  The image requires
you to run the container with exposing the ports required
for the Unifi Controller as well as placing the files into
the /var/lib/unifi location on the container

Here's an example of the run command from my system, you may
need to change the directory for the host volume mount:

```
docker pull supafyn/unifi-controller:latest

docker stop unifi

docker rm -f unifi

docker run -d -p 3478:3478/udp -p 8080:8080 -p 8443:8443 -p 8843:8843 -p 8880:8880 -v /volume1/docker/unifi/:/var/lib/unifi --restart=always --name=unifi --net=host -h unifi supafyn/unifi-controller:latest
```
