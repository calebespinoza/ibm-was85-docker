# IBM Websphere Application Server on Docker
This repo provides Dockerfiles in order to create Docker Images provisionated with WAS 8.5.

## Folders
* CentOS
Use this Dockerfile to provision a CentOS 7 image.
* Ubuntu
Use this Dockerfile to provision a Ubuntu 18 image.

## Create a Docker Image
```
cd CentOS
```

```
docker build -t docker_hub_repo/image_name:version --build-arg ibmUser=yourUserName --build-arg ibmPass=yourPassword .
```