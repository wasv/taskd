
# Taskwarrior for Docker

This is a docker image for the Taskwarrior
[Taskserver](https://github.com/GothenburgBitFactory/taskserver).

This is a fork of [lukasdietrich/taskwarrior-docker](https://github.com/lukasdietrich/taskwarrior-docker)
that I am customizing for my own use, with added kubernetes config files
modified from [lenalebt's gist](https://gist.github.com/lenalebt/8d60784ad01f209c66cb5c52b8c0091d).

## Docker-Compose

```yaml
version: '2.2'

services:
  taskwarrior:
    container_name: taskwarrior
    image: lukd/taskwarrior

    ports:
      - "53589:53589"

    environment:
      - "TASKD_BITS=4096"
      - "TASKD_EXPIRATION=365"
      - "TASKD_ORGANIZATION=My Organization"
      - "TASKD_CN=taskd.example.com"
      - "TASKD_COUNTRY=SE"
      - "TASKD_STATE=Västra Götaland"
      - "TASKD_LOCALITY=Göteborg"

    volumes:
      - "./volumes/data:/data"
```

### Add Org + User

```sh
$ taskd add org Public
$ taskd add user Public User
$ cd ${TASKDDATA}/pki
$ ./generate.client User
```
