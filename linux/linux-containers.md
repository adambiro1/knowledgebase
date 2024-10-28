# linux-containers



## docker



escalate root privilages in docker, when is user part of docker group:

```
docker run -ti --name hacker --privileged -v /:/host ubi8 chroot /host
```


## podman

Config files:

/usr/share/containers/containers.conf—Where a distribution can define the changes the distribution likes to use /etc/containers/containers.conf—Where they can set up system overrides 

$HOME/.config/containers/containers.conf—Can be specified only in rootless mode

run shell in container:

```
podman run -ti --rm registry.access.redhat.com/ubi8/httpd-24 
```

run an containerized application:

```
podman run -d -p 8080:8080 --name myapp registry.access.redhat.com/ubi8/httpd-24
```

stop container:

```
podman stop <containername> #can use --all or --latest 
```

or

```
podman kill <containername>
```

start container:

```
podman start <container name>
```


>all—This starts all of the stopped containers in container storage.
--attach—This attaches your terminal to the output of the container.
--interactive (-i)—This attaches the terminal input to the container.


Inspect container:

```
podman inspect myapp
```

Inspect specified command to execute container:

```
podman inspect --format '{{ .Config.Cmd }}' myapp
```

Inspecting the stop signal to be used when stopping the container:

```
podman inspect --format '{{ .Config.StopSignal }}' myapp
```

**exec-ing into a container** while it is still running**:**

```
podman exec -i myapp  -c 'cat > /var/www/html/index.html' << _EOF
<html>
<head>
</head>
<body>
<h1>Hello World</h1>
</body>
</html>
_EOF
```


>tty—This connects a -tty to the exec session.
--interactive—The -i option tells Podman to run in interactive mode, mean-
ing you can interact with an exec-ed program, like a shell.


execute command/start process in running containter:

```
podman exec myapp cat /var/www/html/index.html
```

man podman-exec

## Creating an image from a container

1. stop container

```
podman stop myimage
```

1. create an image

```
podman commit myapp myimage
```

create a new container based on an image:

```
podman run -d --name myapp1 -p 8080:8080 myimage
```


> --pause—This pauses a running container during the commit. 
The podman pause and podman unpause commands allow you to pause and
unpause containers directly.

> --change—This option allows you to commit instructions on using the image.
The instructions are CMD, ENTRYPOINT, ENV, EXPOSE, LABEL, ONBUILD, STOPSIGNAL, USER, VOLUME, and WORKDIR. These instructions match up with the directives in the Containerfile or Dockerfile



 Using the podman commit command to create an image is not a com-
mon method. The entire process of building container images can be
scripted and automated using podman build.


`man podman-commit`

## Working with container images

Show image tree:

```
podman image tree myimage
```

see the actual files and directories that have been changed:

```
podman image diff myimage ubi8/httpd-24
```

list all images:

```
podman images --all
```

inspect images:

```
podman image inspect myimage
```

default command to be executed from this image:

```
podman image inspect --format '{{ .Config.Cmd }}' myimage
```

see the stop signal:

```
podman image inspect --format '{{ .Config.StopSignal }}' myimage
```

### podman login

```
podman login quay.io
```

credentials are stored in /run/user/$UID/containers/auth.json file

so it is important to user encrypted password

logout of registry:

```
podman logout quay.io
```

### Pushing images

push image to repo:

```
podman push myimage quay.io/username/myimage
```

tag image:

```
podman tag myimage quay.io/username/myimage
```

tag image with version:

```
podman tag myimage quay.io/username/myimage quay.io/username/myimage:1.0
```

push version of an image to repo:

```
podman push quay.iousername/myimage:1.0
```

remove all images:

```
podman image prune -a
```

when it does not work remove it with id:

```
podman rmi 8e8dd226f518 --force
```


 when there are multiple tags it does not want to delete a container


pull image:

```
podman pull quay.io/username/myimage
```

shortname aliases for registries in /etc/containers/registries.conf.d/000-shortnames.conf

## Building images

automating building of an application:

```
mkdir myapp
```

```
cat > myapp/index.html << _EOF
<html>
<head>
</head>
<body>
<h1>Hello World</h1>
</body>
</html>
_EOF
```

```
cat > myapp/Containerfile << _EOF
FROM ubi8/httpd-24
COPY index.html /var/www/html/index.html
_EOF
```

```
podman build -t quay.io/username/myimage ./myapp/
```

add some CI/CD system

```
cat > myapp/automate.sh << _EOF
#!/bin/
podman build -t quay.io/username/myimage ./myapp
podman push quay.io/username/myimage
_EOF
$ chmod +x myapp/automate.sh
```

add some automation scripts

## Volumes

mount storage to contianer:

```
podman run -d -v ./html:/var/www/html:ro,z -p 8080:8080 quay.io/username/myimage
```


 :ro means readonly mode


**Named volumes**

create a volume:

```
podman volume create webdata
```

inspect volume:

```
podman volume inspect webdata
```

it creates a dir in local container storage: */home/user/.local/share/containers/storage/volumes/webdata/_data*

create content from the host in this directory:

```
cat > /home/user/.local/share/containers/storage/volumes/webdata/_data/index.html << _EOL
<html>
<head>
</head>
<body>
<h1>Goodbye World</h1>
</body>
</html>
_EOL
```

run the myimage application using this volume:

```
podman run -d -v  webdata:/var/www/html:ro,z -p 8080:8080 quay.io/username/myimage
```

remove volume:

```
podman volume rm --force webdata
```

list volumes:

```
podman volume list
```

**mount options**

lowercase z option tells Podman to relabel the content with SELinux labels that will allow multiple containers to read and write in the volume:

```
podman run -d -v ./html:/var/www/html:ro,z -p 8080:8080 quay.io/username/myimage
```

**U volume option**

user namespace mapping looks like this:

```
podman unshare cat /proc/self/uid_map
```

when you need to set ownership of the directory to some other uid do this:

```
podman unshare chown 60:60 ./html
```


 Many container images exist with the default UID defined in them.


```
podman run docker.io/mariadb grep mysql /etc/passwd
```


 The U option tellsPodman to recursively change ownership (chown) the source volume to match the default UID the container executes with.


create dir  for database:

```
mkdir mariadb
```

check ownership:

```
ls -ld mariadb/
```

run the mariadb container with the --user mysql, and bind mount the ./mari-
adb directory to /var/lib/mariadb with the :U option. The directory is now
owned by the mysql user:

```
podman run --user mysql -v ./mariadb:/var/lib/mariadb:U docker.io/mariadb ls -ld /var/lib/mariadb
```

the mariadb dir is now owned by different uid:

```
ls -ld mariadb/
```

**selinux option**


 lowercase z command option tells Podman to recursively relabel all content in the source directory with a label that can be read and written by all containers from an SELinux point of view. If the volume will not be used by more than one container, relabeling with the lowercase z option isn’t what you want. If a different hostile container escapes confinement, it might be able to access this data and read/write it. Podman provides an uppercase Z option that tells Podman to recursively relabel the content in such a way that only the processes within the container can read/write the content.


disable SELinux enforcement for container separation to allow the containers to use the volume:

```
podman run --security-opt label=disable -v /home/user:/home/user -p 8080:8080 quay.io/username/myimage
```

## Running pods

create a pod:

```
podman pod create -p 8080:8080 --name mypod --volume ./html:/var/www/html:z
```

Adding a container to a pod:

```
podman create --pod mypod --name myapp quay.io/username/myimage
```

create second container:

```
podman create --pod mypod --name time --workdir /var/www/html ubi8 ./time.sh
```

start pod:

```
podman pod start mypod
```

stop pod:

```
podman pod stop mypod
```

list pods:

```
podman pod list
```

remove pod:

```
podman pod rm mypod
```