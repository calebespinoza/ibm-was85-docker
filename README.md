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

## Documentation

* [IBM Storing Credentials](https://www.ibm.com/support/knowledgecenter/SSDV2W_1.8.4/com.ibm.cic.commandline.doc/topics/t_imcl_store_credentials.html)

* [IBM imcl Command Arguments](https://www.ibm.com/support/knowledgecenter/en/SSDV2W_1.8.4/com.ibm.cic.commandline.doc/topics/r_tools_imcl.html)
