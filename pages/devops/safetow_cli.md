---
title: SafeTow CLI
last_updated: July 2019
sidebar: primary_sidebar
permalink: devops_safetow_cli.html
folder: devops
---

## Overview

The SafeTow CLI is a command-line-interface tool that manages the manual tasks associated with the DevOps process in the cloud. It is not used for local development tasks.

__All of the manual commands involved in managing the docker containers and kubernetes clusters should be solved with this command tool.__

It is broken up into two main files `safetow.rb` and `safetow_module.rb` found in the root of the "safetow-rails" folder.
- `safetow.rb` contains the code and logic for the commands and options associated with what you input into the command line.
- `safetow_module.rb` contains all of the methods and logic that are run from the arguments in the main file. 

The following is the output of the help file:

```sh
2019
SafeTow CLI v01

Variables:
target => [app, db, all]
env => [development, test, staging, sales, production]

Commands:
  -b, --build=<s+>              --build target, Build dockerfile and update in AWS
  -s, --start=<s+>              --start target env, Kubernetes start target
  -t, --stop=<s+>               --stop target env, Kubernetes stop target
  -u, --update=<s+>             --update target env, Kubernetes update target 
  -a, --status=<s+>             --status target env, Kubernetes status target
  -e, --set_domain_name=<s+>    --set_domain_name
  -h, --help                    Show this message
```

## Arguments

### target

This value can resolve to either `app`, `db`, or `all`. 
- `app` means that the action is being taken on the Ruby on Rails project, the 'safetow-rails' directory root dockerfile
- `db` means the action is taken on the Neo4J database, with the _'docker_config_data/neo4j'_ dockerfile
- `all` means that the action is taken on both the application and the database

### env

This is the environment variable that the action is taken on. The environment variable is managed with __configmaps__ 

## SafeTow Module Methods

### check_kops_status

__Command__

`kops get clusters --state s3://kubernetes.safetow.network`

__Parameters__

N/A

__Description__

This method runs the `kops` cli which tells us the kops service is running and able to access our Kubernetes cluster.

### check_kubectl_status

__Command__

`kubectl config current-context`

__Parameters__

N/A

__Description__

This method evaluates to our current context (_https://app.safetow.network_) and ensures that the `kubectl` command-line tool is working properly.


### login_aws_ecr

__Command__

`$(aws ecr get-login --no-include-email --region us-east-1)`

__Parameters__

N/A

__Description__

This method uses the `aws` command line interface to ensure that the active terminal user is signed into ECR (elastic container registry) where the dockerfiles are kept and stored.

### build_safetow_dockerfile

__Command__

`docker build -t safetow .`

__Parameters__

N/A

__Description__

Builds the dockerfile at the project root of the Ruby on Rails SafeTow application.

### tag_safetow_dockerfile

__Command__

`docker tag safetow:latest 887106411854.dkr.ecr.us-east-1.amazonaws.com/safetow:latest`

__Parameters__

N/A

__Description__

Takes the built dockerfile stored in memory and gives it a tag of the URL to the ECR path to which it should be pushed to.

### push_safetow_dockerfile

__Command__

`docker push 887106411854.dkr.ecr.us-east-1.amazonaws.com/safetow:latest`

__Parameters__

N/A

__Description__

Pushes the built and tagged dockerfile to AWS ECR.

### build_neo4j_dockerfile

__Command__

`docker build -t safetow-neo4j docker-config-data/neo4j/`

__Parameters__

N/A

__Description__

Builds the dockerfile of the Neo4j container to be used with SafeTow.

### tag_neo4j_dockerfile

__Command__

`docker tag safetow-neo4j:latest 887106411854.dkr.ecr.us-east-1.amazonaws.com/safetow-neo4j:latest`

__Parameters__

N/A

__Description__

Takes the built dockerfile stored in memory and gives it a tag of the URL to the ECR path to which it should be pushed to.

### push_neo4j_dockerfile

__Command__

`docker push 887106411854.dkr.ecr.us-east-1.amazonaws.com/safetow-neo4j:latest`

__Parameters__

N/A

__Description__

Pushes the built and tagged dockerfile to AWS ECR.

### kubernetes_get_all

__Command__

`kubectl get all`

__Parameters__

N/A

__Description__

Returns all kubernetes objects from a cluster that are currently running. This is made up of the nodes, services and deployments. The following excerpt is an example of what would be returned.

```
NAME                                 READY   STATUS    RESTARTS   AGE
pod/safetow-d47f87b6b-2q4s2          1/1     Running   0          2d
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
```

This is useful for diagnosing problems at a glance. For more specific tasks beyond this point of troubleshooting, it is recommended to go directly into `kubectl` commands rather than depend on the SafeTow CLI.

### start_neo4j_kubernetes

__Command__

`kubectl create -f kubernetes-safetow-neo4j.yml`

__Parameters__

N/A

__Description__

This method creates the objects defined in the local __kubernetes-safetow-neo4j.yml__ file and creates them on the active cluster, which is kubernetes.safetow.network.


### start_safetow_kubernetes

__Command__

`kubectl create -f kubernetes-safetow-rails.yml`

__Parameters__

N/A

__Description__

This method creates the objects defined in the local __kubernetes-safetow-rails.yml__ file and creates them on the active cluster, which is kubernetes.safetow.network.

### build(target)

__Command__

/

__Parameters__

target - `db`, `app` or `all`. Defaults to `all`.

__Description__

This method will take the desired target, and build the corresponding dockerfile, tag it, then upload it to AWS ECR.

### start(target, env)

__Command__

/

__Parameters__

target - `db`, `app` or `all`. Defaults to `all`.
env - `development`, `test`, `staging`, `sales`, `demo`, `production`

__Description__

This method will take the desired target, and build the corresponding dockerfile, tag it, then upload it to AWS ECR.

### stop(target, env)

### delete_safetow_deployment

### delete_safetow_service

### delete_neo4j_deployment

### delete_neo4j_service

### delete_neo4j_pvc

### set_environment_configmap(env)

### create_new_configmap(env)

### describe_configmap

### load_balancer_ingress

### set_domain_name

