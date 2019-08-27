---
title: Kubernetes
last_updated: July 2019
sidebar: primary_sidebar
permalink: devops_kubernetes.html
folder: devops
---

This document will go over what we need to discuss in terms of dev ops... important things are:

## What is Kubernetes?

Kubernetes is a __container orchestration tool__. That means that it takes the Docker containers which we set up for our application and database, then co-ordinates them together on the cloud in a way that makes the application managable for us administrators and accessible for our users.

### Example kubernetes cluster

Kubernetes puts together our containers into a __cluster__. We use the cluster with the name `kubernetes.safetow.network`. This cluster's data is being stored in an AWS S3 bucket with a matching name.

The following is the example of a fully operating kubernetes cluster, which would be made available to you through running `kubectl get all` in an active cluster.

```
NAME                                 READY   STATUS    RESTARTS   AGE
pod/safetow-d47f87b6b-2q4s2        1/1     Running   0          2d
pod/safetow-neo4j-7fd57b8749-rftt4   1/1     Running   0          2d

NAME                    TYPE           CLUSTER-IP     EXTERNAL-IP                                                              PORT(S)                                        AGE
service/kubernetes      ClusterIP      100.64.0.1     <none>                                                                   443/TCP                                        87d
service/safetow         LoadBalancer   100.67.1.219   afdfb97f19db311e9ab780a444022e24-689211624.us-east-1.elb.amazonaws.com   80:30037/TCP,443:30455/TCP                     2d
service/safetow-neo4j   NodePort       100.70.51.90   <none>                                                                   7474:30955/TCP,7473:30258/TCP,7687:31291/TCP   2d

NAME                            DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/safetow         1         1         1            1           2d
deployment.apps/safetow-neo4j   1         1         1            1           2d

NAME                                       DESIRED   CURRENT   READY   AGE
replicaset.apps/safetow-d47f87b6b          1         1         1       2d
replicaset.apps/safetow-neo4j-7fd57b8749   1         1         1       2d

NAME             STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
neo4j-pv-claim   Bound    pvc-fe50d09b-9db3-11e9-ab78-0a444022e242   5Gi        RWO            gp2            2d
```

You will notice that the same names are repeated over and over, in this example we have __safetow__ and __safetow-neo4j__.

What is happening is that each of these two labels is corresponding to at least 4 different types of _objects_, these are the __pod__, the __service__, the __deployment__ and the __replicaset__.

The __pod__ is where you can image the "docker container" sitting, as an independent GNU/Linux filesystem (generally Debian) that would resemble a server running the real world. You can SSH into one of these pods through a terminal window and move around in it as if you were on any other machine. You can manipulate files, run programs, do anything you could usually do from your terminal and the changes will be reflected live. If the software running in a pod crashes, it will restart on its own.

The __neo4j-pv-claim__ is a "persistent volume claim" that is attached to the neo4j service, deployment and pod. If the pod crashes and resets, no data is lost because there is a mounted storage volume that sits independently from that pod.

The __deployment__ manages the pods. It defines which docker containers are used in each type of pod, and sets the environment variables to be used in each.

The __service__ contains the data about networking. It describes the access of ports for the corresponding pod and deployments to which it is linked. Notice that only the _service/safetow_ service has an external IP, meaning it can be networked to from the outside world. That long URL is later mapped to our chosen domain name at _app.safetow.network_.

The __replicaset__ ...

The __configmap__ ...

\#TODO finish this explanation

## Kops on AWS

There are many different ways that Kubernetes can be deployed. Each cloud provider has its own method, and you can even run it locally on your own machine. Our solution is to use [Kops](https://github.com/kubernetes/kops).

Kops is an official Kubernetes project for managing production-grade Kubernetes clusters. Kops is currently the best tool to deploy Kubernetes clusters to Amazon Web Services. AWS has its own solution called EKS, but that abstracts away some useful features of kubernetes and has higher pricing and fixed vendor-lock in to Amazon.

Here is a link to the [docs from Kubernetes](https://kubernetes.io/docs/setup/production-environment/tools/kops/) and the [docs from AWS](https://aws.amazon.com/blogs/compute/kubernetes-clusters-aws-kops/) for how to set up KOPS, however I found [this Youtube playlist](https://www.youtube.com/playlist?list=PLaGfdei15ACdNcOjKELO79vnt89RhVKrm) to be the best resource online. In the case that these videos are taken down, I have downloaded copies of them.

### Setup Kops

Following these instructions is required in order to properly interact with the cluster from your local machine. Start with the following commands in your terminal:

```sh
brew update && brew install kops
```

Then, you must ensure that you have Kubernetes installed in your machine. To do this, ensure that you have Docker installed, then from the docker menu enable Kubernetes:

![Docker Kubernetes menu](/images/documentation_images/docker-kubernetes-menu.png)

Then, ensure that you have kubectl installed. You can follow documentation [here](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-on-macos) or simply use this command for macOS with brew:

```sh
brew install kubectl
```


### Kubernetes and AWS S3 Cluster

The links at the top of this section discuss how to walk through setup of the first kubernetes cluster on S3. In the documentation here I will direct you to the existing S3 bucket where I have installed our kubernetes cluster and walk through connecting to it.

First, you must have the __aws command line interface__ installed. The documentation on how to do this is found [here](https://docs.aws.amazon.com/polly/latest/dg/setup-aws-cli.html).

\#TODO give a brief explanation of how to connect to AWS cli and log in as authenticated AWS user with access to proper permissions.

Our S3 bucket link is found [here](https://s3.console.aws.amazon.com/s3/buckets/kubernetes.safetow.network/?region=us-east-1&tab=overview). The files in this bucket should not be manually edited. It is all automatically managed through the command line tools. 

__What is important is that we know the address to our S3 bucket through the AWS command line interface is `s3://kubernetes.safetow.network`.__

Our next commands to run:

```sh
export KOPS_STATE_STORE=s3://kubernetes.safetow.network
```

### Bonus - terminal extensibility

If you are using the default terminal, you will not know at a glance which kubernetes cluster you are actively connected to. Using an alternative terminal such as [fish](https://fishshell.com/) or [zsh](https://ohmyz.sh/) can give you the extensibility of more features that are not in the default "bash" program. 

In the following screenshot you will notice that I have __"kubernetes.safetow.network"__ and __"2.5.0"__ persisted in my command line view at all times. These correspond to __my active kubernetes cluster__ (that _kubectl_ commands will reply to) and __my active ruby version___ (as set by _RVM_, the ruby version manager). 

This is important so that I am always aware of these variables while I am performing command-line tasks. I can also see which folder I am in at any given time without needing to use the `pwd` command.

\#TODO add specific instructions as to how this can be set up.

![Extensible terminal](/images/documentation_images/fish-terminal-k8scluster-rvm.png)

## How to shut down and start up the cluster on AWS

You will be able to see in the AWS EC2 dashboard that "KOPS" is creating new nodes for Kubernetes that are automatically managed and created by the system.

In the below image you will notice that they are labelled by prefixes such as __nodes.__ or __master-[zone].__ and cannot be manually controlled in this setting. If you try to delete the nodes or shut them down, new ones appear in their place.

![AWS EC2 Dashboard](/images/documentation_images/aws_ec2_kubernetes_panel.png)

The way that these instances are managed is that configuration files exist within the scope of the cluster, in our situation that cluster is __kubernetes.safetow.network__.

Keep in mind that Kubernetes is built up with two different types of instances, ones that are the __nodes__ and ones that are the __masters__. 

```sh
kops edit ig nodes --state s3://kubernetes.safetow.network
```

This will open up a file that matches the following contents. You will notice that there are fields here that are labeled as __maxSize__ and __minSize__. These correspond to the number of EC2 instances. You will need to set that number to 0 in order to turn off the EC2 instances. Then once you have saved the document, follow the instructions below to apply the updates.

Keep in mind that this is using the _vim_ file editor. That means you are editing with keyboard controls. Full vim documentation can be found [online](https://www.vim.org/docs.php), however these are a few simple instructions:

- _`:i` to enter 'edit mode.' Navigate with keys down to the line. Type your changes. `:wq!` to save your changes and exit._

```yml
apiVersion: kops/v1alpha2apiVersion:apiVersion:
kind: InstanceGroup
metadata:
  creationTimestamp: 2019-04-09T15:23:13Z
  labels:
    kops.k8s.io/cluster: kubernetes.safetow.network
  name: nodes
spec:
  image: kope.io/k8s-1.10-debian-jessie-amd64-hvm-ebs-2018-08-17
  machineType: t2.medium
  maxSize: 1
  minSize: 1
  nodeLabels:
    kops.k8s.io/instancegroup: nodes
  role: Node
  subnets:
  - us-east-1a
```

Now you can repeat the same process for the "master", where you are once again changing the __maxSize__ and __minSize__ values to the number you desire.

```sh
kops edit ig master-us-east-1a --state s3://kubernetes.safetow.network
```

```yml
apiVersion: kops/v1alpha2
kind: InstanceGroup
metadata:
  creationTimestamp: 2019-04-09T15:23:13Z
  labels:
    kops.k8s.io/cluster: kubernetes.safetow.network
  name: master-us-east-1a
spec:
  image: kope.io/k8s-1.10-debian-jessie-amd64-hvm-ebs-2018-08-17
  machineType: t2.medium
  maxSize: 1
  minSize: 1
  nodeLabels:
    kops.k8s.io/instancegroup: master-us-east-1a
  role: Master
  subnets:
  - us-east-1a
```

Then run the following two commands, one after another. The changes will be applied within a few minutes.

```sh
kops update cluster --yes --state s3://kubernetes.safetow.network
kops rolling-update cluster --yes --state s3://kubernetes.safetow.network
```

## Docker Containers hosted on AWS

When working with Kubernetes, the docker containers which will be orchestrated together cannot only exist locally on your machine. They must exist hosted in a cloud solution.

We have our docker containers stored on AWS's ECR. The link to our containers is [found here](https://console.aws.amazon.com/ecr/repositories?region=us-east-1). We have two set up:
- [safetow](https://console.aws.amazon.com/ecr/repositories/safetow/?region=us-east-1): corresponding to the safetow-rails application.
- [safetow-neo4j](https://console.aws.amazon.com/ecr/repositories/safetow-neo4j/?region=us-east-1): corresponding to the Neo4J database configured to run with SafeTow.

In the configuration file below, you will see that when setting up containers, they point to the addresses of `887106411854.dkr.ecr.us-east-1.amazonaws.com/safetow` and `887106411854.dkr.ecr.us-east-1.amazonaws.com/safetow-neo4j`.

## Kubernetes object project configuration files

We have to set up .yml files for Kubernetes to work with and understand. The documentation from Kubernetes about how this is set up is found [here](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/).

We have two files to manage this: __kubernetes-safetow-rails.yml__ and __kubernetes-safetow-neo4j.yml__. They each contain multiple objects, grouped by which aspect of the application they pertain to. I will now give an overview of an explanation of the contents of each file and which objects are included and why.

By default, all of these objects are networked into a single group. If we wanted to make things more complicated, we could set up multiple dedicated "networks" that only certain objects could communicate with eachother. This would be useful in a long-term approach to a microservices architecture but is not directly applicable to what we are doing now.

These objects all make up our "cluster", which is found at the address `s3://kubernetes.safetow.network`. It is all in the corresponding S3 storage bucket.

### kubernetes-safetow-rails.yml

```yml 
# SAFETOW SERVICE
apiVersion: v1
kind: Service
metadata:
  name: safetow
  labels:
    app: safetow
  annotations:
    # Note that the backend talks over HTTP.
    service.beta.kubernetes.io/aws-load-balancer-backend-protocol: http
    # TODO: Fill in with the ARN of your certificate.
    service.beta.kubernetes.io/aws-load-balancer-ssl-cert: arn:aws:acm:us-east-1:887106411854:certificate/a8d53383-b401-4c76-9639-dd293f944fc6
    # Only run SSL on the port named "https" below.
    service.beta.kubernetes.io/aws-load-balancer-ssl-ports: "https"
spec:
  ports:
  - port: 80
    name: http
    # Use named container port.
    targetPort: backend-http
  - port: 443
    name: https
    # Use named container port.
    targetPort: backend-http
  selector:
    app: safetow
    tier: frontend
  type: LoadBalancer
---
# SAFETOW DEPLOYMENT
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: safetow
  labels:
    app: safetow
    env: default-env
spec:
  replicas: 1
  selector:
    matchLabels:
      app: safetow
      tier: frontend
  template:
    metadata:
      labels:
        app: safetow
        tier: frontend
    spec:
      containers:
      - name: safetow
        image: 887106411854.dkr.ecr.us-east-1.amazonaws.com/safetow
        imagePullPolicy: Always
        ports:
        - containerPort: 3000
          # This name will be used in the Service.
          name: backend-http
        env:
          - name: DB_URL
            value: http://neo4j:password@safetow-neo4j:7474
          - name: ENVIRONMENT_VARIABLE
            valueFrom:
              configMapKeyRef:
                # The ConfigMap containing the value you want to assign to SPECIAL_LEVEL_KEY
                name: safetow-configmap
                # Specify the key associated with the value
                key: environment.variable

```

The __SAFETOW SERVICE__ is set up with an AWS load balancer to communicate with the outside world. 
- SSL certificate is set up in AWS, and referenced here.
- Additional code outlined in the [SafeTow CLI](/devops_safetow_cli.html) highlights how the load balancer routes into the final URL of _"https://safetow.network"_
- Our mobile clients access the application at _"https://safetow.network"_ and display the content from there over port 443.

The __SAFETOW DEPLOYMENT__ is our SafeTow Ruby on Rails application
- The referenced _safetow-configmap_ is generated as part of our [SafeTow CLI](/devops_safetow_cli.html), where the environmnet variable is set at startup as "demo", "staging", "production", etc.
- \#TODO Right now only one version of SafeTow can be deployed at the time, future extensibility will program in multiple environments being managed at different URLS with different environments running simoutaneously.
- The default username and passphrase used to access the neo4j server is neo4j:password. It is essential to have some level of authentication which can be accessed, but nothing except a kubernetes object which we build would even have access to the port 7474 in the Kubernetes object for the Neo4J database.

### kubernetes-safetow-neo4j.yml

```yml
# NEO4J SERVICE
apiVersion: v1
kind: Service
metadata:
  name: safetow-neo4j
  labels:
    app: safetow
spec:
  ports:
  - name: "7474"
    port: 7474
    targetPort: 7474
  - name: "7473"
    port: 7473
    targetPort: 7473
  - name: "7687"
    port: 7687
    targetPort: 7687
  selector:
    app: safetow
    tier: neo4j
  type: NodePort
---
# NEO4J PERSISTENT VOLUME
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: neo4j-pv-claim
  labels:
    app: safetow
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
---
# NEO4J DEPLOYMENT
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: safetow-neo4j
  labels:
    app: safetow
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: safetow
        tier: neo4j
    spec:
      containers:
      - name: neo4j
        image: 887106411854.dkr.ecr.us-east-1.amazonaws.com/safetow-neo4j
        imagePullPolicy: Always
        ports:
        - containerPort: 7474
        - containerPort: 7473
        - containerPort: 7687
        volumeMounts:
        - name: neo4j-persistent-storage
          mountPath: /data
      imagePullSecrets:
        - name: awsecr-cred
      volumes:
      - name: neo4j-persistent-storage
        persistentVolumeClaim:
          claimName: neo4j-pv-claim
```

This file contains all of the configuration for the Neo4J database.

The __NEO4J SERVICE__ is what exposes the ports that makes them accessible.
- We opened up the ports where Neo4J wants to communicate (7474, 7473, 7687).
- These ports can only be accessed from the other objects within our cluster, no external services can access it.
- \#TODO create a way to directly access the Neo4J database externally to run queries and monitoring systems such as Prometheus.

The __NEO4J PERSISTENT VOLUME__ is where the data is stored. 
- It is stored outside of the object where the actual application is hosted. That means that the database can crash, restart, upgrade to a new version, etc. and we will not lose the data.
- We gave it a capacity of 5 gigabytes. We can extend this and resize it without losing data in the future as the application grows. Our biggest data
- \#TODO create a system of backups that takes the volume and stores to an S3 bucket and offline system.

The __NEO4J DEPLOYMENT__ contains the Neo4J application.
- It references a container where there is a specific image. That image is the dockerfile which we created and stored on Amazon's ECS. 
- It references our persistent volume claim for the /data directory in the container to resolve to our 























