# Vagrant

## Building a Vagrant Box from CentOS7 

### vagrant box add
```
$ vagrant box add centos75.box --name {box_name}
```
### update Vagrant file(※手元にあったら要らない)
```
in Vagrantfile
 
 - skip -
 config.vm.box = "write_your_box_name"
 - skip -

```
### vagrant up and ssh
```
$ vagrant up
$ vagrant ssh
```
## docker install

### yum update
```
$ sudo yum update
```

### docker packages
```
$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

### docker repository
```
$ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

### update yum package index
```
$ sudo yum makecache fast
```

### docker install(latest)
```
$ sudo yum install docker-ce
```

### check docker version
```
$ docker -v

Docker version xx.xx.x, build xxxxxxxxxx
```

### docker start
```
$ sudo systemctl start docker
```

### Setting to automatically start Docker at OS startup
```
$ sudo systemctl enable docker
```

### if you don't want to using 'sudo' every time, please add Docker group in your USER 
```
dockerグループはすでにあるはずだけど念の為
$ sudo groupadd docker
現在のユーザーをdockerグループに入れる
$ sudo usermod -aG docker $USER
docker restart
$ sudo systemctl restart docker
一回出てから反映される
$ exit
```