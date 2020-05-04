# IBM Developer NY Meetup May 2020

## Container and Container Orchestration

This is a very simple demo application to demonstrate container technologies and container orchestration. Hopefully by the end of this we will all learn some useful basics. 

## Sign Up for a cloud account
 https://ibm.biz/BdqF8K 

## Docker

Docker is almost synonymous with container technologies and for good reason. They were one of the first in the industry to make it easy for developers to create containers.

## Kubernetes

Kubernetes is a container orchestrator. In simple terms what it means is that it makes sure containers run in the given infrastructure. It does much more than that but for our use case this is enough. 

## The Application

Full disclaimer I am not a python developer. But when I thought about creating this demo I thought what language would be most accessible to most attendees. Python was the clear winner.

The application is quite simple. I have a list of quotes. Everytime you visit the page at path /hello/{name} it will show you one quote and its author.

## Dockerfile

To create the docker container for this application we have the Dockerfile. The content of the file is as follows.

```
FROM python:alpine3.7

WORKDIR /app

COPY requirements.txt /app

RUN pip install --trusted-host pypi.python.org -r requirements.txt 

COPY . /app

EXPOSE 80

ENTRYPOINT [ "python" ]

CMD [ "./hello.py" ]
```

This is pretty straight forward as dockerfiles go. 

## Build the docker image

```
docker build -t <username>/<imagename>:<tag> .
```

## Push it to dockerhub

```
docker login
```

```
docker push <username>/<imagename>:<tag>
```

## Private registry

Public dockerhub is great for learning about docker images and getting other people to easily use and access your application. But when you are writing software you don't want just any one to access, you would want to use a private registry. 

IBM Cloud gives you a free image registry.

## Kubernetes

Go to cloud shell

```
https://workshop.shell.cloud.ibm.com/
```

If it asks for a key use `ikslab`.

Login to your IBM Cloud account. In your dashboard you should see a cluster. 

```
ibmcloud ks clusters
```

This would list all the clusters. You should see only one.

```
ibmcloud ks cluster-config -c $CLUSTER-NAME
```

This will print a `export KUBECONFIG=...` command. Copy and paste that in your terminal.

This sets the `kubectl` with the right config.

## Deployments

Apply the deployment

```
kubectl apply -f k8s/deployment.yaml
```

## Service

Apply the service

```
kubectl apply -f k8s/service.yaml
```
