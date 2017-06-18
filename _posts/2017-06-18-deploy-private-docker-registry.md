---
layout: post
published: true
title: Deploy your own private docker registry 2017
mathjax: false
featured: true
comments: false
headline: Deploy your own private docker registry (distribution)
categories: 
  - devops
tags: devops docker aws gcp Kubernetes
---

Software        | Version
--------------- | -------------
Docker          | >= 1.6.0

<p style="text-align: center;"><img src="https://www.devopszen.com/images/blog/docker-registry.png" /></p>

Before moving the stack into Kubernetes, you might think about mangage a private docker registry. Docker registry is imporant in your Kubernetes CI/CD pipeline. This article shows how to deploy a private docker registry with S3 storage and legency disk space.

By default, docker engine uses the docker images at [https://hub.docker.com/](https://hub.docker.com/). But you can use docker images prefix with domain name, port number such as localhost:5000/myimage.

### The benefit of mantain a private docker registry

* Fully owned images and full control
* Integrate with your own deployment pipeline and development workflow
* Privacy and security
* Cost efficient


Docker had renamed the project of docker registry to be Docker Distribution, which is rewritten with Golang for performance reason. The project location is [https://github.com/docker/distribution](https://github.com/docker/distribution). 

### How to deploy your own private docker registry

```
docker run -d -p 5000:5000 --restart=always --name registry \
  -v `pwd`/data:/var/lib/registry \
  registry:2
```

Then you can access the private docker registry with location localhost:5000/

### Private Docker registry Authenticate

You can put nginx at the front of docker registry and setup the authenticate at Nginx.

### Docker registry disk space clean up and GC

Docker registry only store the same docker layers once. Users can delete a particular layer which is just marking the layer can be GC.

**Docker registry GC**

```
bin/registry garbage-collect [--dry-run] /path/to/config.yml
```

### How to use the private docker registry

**Pull images from Docker Hub public registry**

```
docker pull ubuntu
```

**Create tag of the image on the private registry**

```
docker tag myimage localhost:5000/myimage
```

**Push the image to the private registry**

```
docker push localhost:5000/myimage
```

**Search image**

```
docker search localhost:5000/alpine
```

### Alternative docker registry solutions

**Google container registry**

Google only charege the storage and network egress, if you are running the system inside Google Cloud, this could be a better choice: [https://cloud.google.com/container-registry/pricing](https://cloud.google.com/container-registry/pricing)

**AWS EC2 Container registry**

AWS fully managed docker container registry also only charge the storage and data transferred to the internet:
[https://aws.amazon.com/ecr/](https://aws.amazon.com/ecr/)

### Reference

* [https://docs.docker.com/registry/](https://docs.docker.com/registry/)
* [https://github.com/docker/distribution](https://github.com/docker/distribution)
* [https://docs.docker.com/registry/recipes/nginx/#setting-things-up](https://docs.docker.com/registry/recipes/nginx/#setting-things-up)
* [https://github.com/docker/docker.github.io/blob/master/registry/deploying.md](https://github.com/docker/docker.github.io/blob/master/registry/deploying.md)
* [https://docs.docker.com/registry/garbage-collection/#how-garbage-collection-works](https://docs.docker.com/registry/garbage-collection/#how-garbage-collection-works)
* [https://www.digitalocean.com/community/tutorials/how-to-set-up-a-private-docker-registry-on-ubuntu-14-04](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-private-docker-registry-on-ubuntu-14-04)

