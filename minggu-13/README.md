# Minggu 13
### Docker Swarm 

1. buka docker
2. Membuat VMs dengan nama vm1 dan vm2
```
$ docker-machine create --driver virtualbox vm1
Running pre-create checks...
(vm1) Default Boot2Docker ISO is out-of-date, downloading the latest release...
(vm1) Latest release for github.com/boot2docker/boot2docker is v19.03.5
(vm1) Downloading C:\Users\ademin\.docker\machine\cache\boot2docker.iso from https://github.com/boot2docker/boot2docker/releases/download/v19.03.5/boot2docker.iso...

$ docker-machine create --driver virtualbox vm2
Running pre-create checks...
(vm2) Default Boot2Docker ISO is out-of-date, downloading the latest release...
(vm2) Latest release for github.com/boot2docker/boot2docker is v19.03.5
(vm2) Downloading C:\Users\ademin\.docker\machine\cache\boot2docker.iso from https://github.com/boot2docker/boot2docker/releases/download/v19.03.5/boot2docker.iso...
(vm2) 0%.Error removing file: Error removing temporary download file: remove C:\Users\ademin\.docker\machine\cache\boot2docker.iso.tmp795909739: The process cannot access the file because it is being used by another process.
(vm2)
Error with pre-create check: "read tcp 192.168.8.103:56198->52.216.206.211:443: wsarecv: An existing connection was forcibly closed by the remote host."

```

