# Overview

Open source container orchestration system initially developed and used at Google.

# kubectl

The `--help` flag accepts a RESOURCE as well, however, the help provided might be generic to the action.

All are prefaced by `kubectl`

    cluster-info

basic information about running cluster

    cluster-info dump

Provides more detail

-

    delete < RESOURCE > < NAME >

Resources can be a comma separated (no spaces) list for multiple types with the same name or `-l` labels.

A file can also be specified (yaml or json).

## describe

`describe <resource type>`

Enumerates key details for resources matching the request. Flags enable various types of filtering.

## exec

`exec < POD > < COMMAND >`

Execute a command on the first container in a `pod`. Passing the `-c` flag allows the specifying of a container other than the first. `-it` can be passed to attach to stdin/stdout.

A common pattern is:

`kubectl exec -it <pod_name> -- /bin/sh`

or:

`kubectl exec -it <pod_name> --container <container_name> -- /bin/sh`

or:

`kubectl exec -it <pod_name> -c <container_name> -- /bin/sh`

## expose

`expose < RESOURCE TYPE > < RESOURCE NAME > --port=80 --target-port=8000`

This resource would serve on port 80 and connect to containers on port 8000.

It is also possible to pass a file

`expose file_describing_resource.yaml --port=80 --target-port=8000`

The file can be either yaml or json, and fields that may be used are defined by the api.

## get

`get < RESOURCE TYPE >`

List resources, such as nodes, deployments, pods etc. `--help` will provide a complete list of such resources.

## label

`label < RESOURCE TYPE > < NAME >`

Apply, or `--overwrite` labels. As with other commands, a json or yaml file may be specified. Note that a label can be removed entirely by a trailing `-`

`kubectl label pod web-1 bye-`

Which would remove the label `bye` from the web-1 pod. However, as these are key/value pairs this does not seem particularly common except to correct errors.  Consider the case of using `version=1.0.2` or `status=healthy` or `env=prod` as examples. In all these cases, the expectation is that the label value would change, but the label itself would remain.

## logs

`logs POD -c CONTAINER`

`-f` allows you to follow that log (all entries).

`--tail=n` where n is number of recent logs to show, and -1 is equivalent to `-f`

`kubectl logs -f pod_name | grep -v "lines_to_ignore include this text"` is a useful pattern to cut down on noise.

Container may be omitted if there is only one in the pod. There are numerous flags to constrain the output, or to `-f` follow it. By default a "snapshot" is returned (according to `--help` without any description of what that means).

## rollout

`rollout SUBCOMMAND RESOURCE_TYPE/NAME`

Subcommands include:

```
history
pause
resume
status
undo
```

Details on each subcommand are available using `--help`.

## run

`run DEPLOYMENT_NAME --image=<repo url> --port=<port number>`

Under the name provided, the master scheduled the creation of the container by the Node, which creates the Pod and containers specified.

## scale

`scale RESOUCE_TYPE/RESOURCE_NAME --replicas=COUNT`

Resource types are Deployment, ReplicaSet, Replication Controller, or Job.

A file may also be used:

`scale -f FILE.yaml --replicas=COUNT`


## set image

`set image TYPE/NAME CONTAINER_NAME=IMAGE`

The image may be a standard docker registry image or a path to an image in a private repository may be provided.

> Note: `set` is a broader command presently operating ONLY on `image`.


## expose

Creates a service from a deploy, svc, rs, rc, or po on the specified port, defaulting to a ClusterIP type.

The following is a quick way to stand up an nginx deploy/rs of two po behind a svc, using NodePort:

```
kubectl run nginx --replicas=2 --image=nginx
kubectl expose deploy/nginx --type=NodePort --port=80
```

## get

cm,deploy,ing,po,rs,rc,sa,svc

Valid resource types include:

- clusters (valid only for federation apiservers)
- componentstatuses (aka 'cs')
- configmaps (aka 'cm')
- daemonsets (aka 'ds')
- deployments (aka 'deploy')
- endpoints (aka 'ep')
- events (aka 'ev')
- horizontalpodautoscalers (aka 'hpa')
- ingresses (aka 'ing')
- jobs
- limitranges (aka 'limits')
- namespaces (aka 'ns')
- networkpolicies
- nodes (aka 'no')
- persistentvolumeclaims (aka 'pvc')
- persistentvolumes (aka 'pv')
- pods (aka 'po')
- podsecuritypolicies (aka 'psp')
- podtemplates
- replicasets (aka 'rs')
- replicationcontrollers (aka 'rc')
- resourcequotas (aka 'quota')
- secrets
- serviceaccounts (aka 'sa')
- services (aka 'svc')
- statefulsets
- storageclasses
- thirdpartyresources

When listing all resources of interest, to focus use `grep -v`, e.g. see all pods that do not have age in terms of days:

```
kubectl get po | grep -v "[0-9]d"
# or use perl regex
kubectl get po | grep -P -v "\dd"
```

Or, to look a bit more precisely with clear age contrast when grep is using color:

`kubectl get po | grep -P " \ds| \d\ds| \dh| \d\dh| \d\dm| \dm"`


# Useful and to be expanded on...

`kubectl delete pod NAME --grace-period=0`

`kubectl get deployments --all-namespaces`

you could then target another command by namespace as in:

`kubectl --namespace=foo delete deployment baz`


# Core Objects / Terms

## Annotations

Key Value maps of meatadata attached to objects. Not used to select objects, contrast with Labels.

This is an easy way to add data to the k8s object so that services within the cluster can understand details about the object asside from the selection.

## Clusters

A collection of resources including:

### Master

Coordinates activities of the cluster.

Exposes an API for the Nodes to use.

### Nodes

VM or physical computer (not just container?).

Docker or rkt.

There should be at least three nodes.

Nodes communicate with the master via the k8s API.

#### kublet

An agent for managing the node and communicating with the cluster.

#### Containerization - docker or rkt

#### Pods

Pods are the atomic unit in k8s. Containers are deployed _within_ a pod. The pod has:

* container specific runtime information such as:
  - ports to use
  - image version
* A cluster specific IP address for networking, meaning multiple containers can share that IP
* Shared storage, as Volumes

> Note on Volumes: Volumes have a life span equal to that of the pod that contains them. This means that other (application) container restarts will not mean the loss of data stored on the volume, however, loss of the pod WILL -- unless the Volume is a mounted resources such as a Amazon Elastic Block Store or a Network File System (NSF) resource.

Pods are _logical hosts_, and the containers within the pod will typically be tightly coupled.


## Deployments

Containerized applications that run on top of clusters. The master schedules the application instances and these are actually created by the individual nodes. So the deployment lives in the master, and the apps live in the nodes.

## Ports

A `port` makes a service visible within a cluster.

A `targetPort` the actual port on the pod.

A `nodePort` the port that kube-proxy is aware of.  

## Services

A logical set of pods that are grouped to allow access via an IP provided outside the cluster.

Services also make service discovery within the cluster possible, meaning that the front end web app and the back end rest server apps (regardless of the number of containers) use the internal cluster unique ip to communicate. Additionally, and external IP can be exposed beyond the cluster (load balancing) or via port using NAT. (This is a bit hand wavey in the the tutorial.)

>Note: Federated Services
>
>It is possible to provided an abstracted _federated_ service that provides one control plane that fronts multiple clusters - for example geographically distinct data centers. This is done by having that federated server front requests to the abstracted clusters in which it creates identical pods in each cluster.

## Labels

Used by k8s to identify a resource and/or as part of a query ops personell perform on a cluster.

Key/value pairs that may be attached to some objects (i.e. pods) and then used as a selector by another (i.e a service). Selectors are applied at deployment, labels may be added at creation or modified later.

Labels are also used by k8s to select objects - contrast with Annotations.



# Resources, Community and Extensions

A collection of Kubernetes specific content that is not part of Vanilla Kubernetes.

## Brigade

An in-cluster event-based scripting of Kubernetes piplines. Brigade offers an API Gateway that can accept events/triggers (GitHub webhook events are supported out of the box) and then deploy a Build of one or more Jobs to accomplish a result. For example, a git commit could trigger a webhook to the API Gateway that would result in the running of *cluster based* tests.

## Draft

A tool that uses Docker, Helm and (usually) mini-kube to let a dev poke and prod at thier containers within a cluster. 

## Helm

A package manager for Kubernetes that simplifies organizing resources as templates and high level configuration (values.yaml) that can be repeatedly rendered and deployed, version controlled, rolled back, and modularized in an extensible manner. 

`helm install foo -f values_file.yaml`  Apply a values file during install


## Openshift 

OpenShift adds many things to Kubernetes

### Build Configuration

Docker builds often run as root. The additional build interface may provide some security beneifits.

Getting from source to image.

### Deployment Configuration

Partial or complete deploymet/re-deployment based on:
- Image change (tag)
- Code change (webhook)
- Config change

### Image Stream

### Integrated Docker Registry

## Logging is EFK

A common logging solution in k8s appears to be Elasticsearch (document storage/search engine), Logstash (log parsing), and Kibana (visualization).

For OpenShift, Logstash is replaced with Fluentd (CNCF).

### Policies are expanded

### Project

A project wraps a namespace and controlls access to that namespace. This appears to be where RBAC was implemented. It is not clear if Projects offer more than simply an abstraction on top of RBAC (that would be fine, though it would be nice to know for sure).

### Routes

Default router is HAProxy.

Route is a construct to define rules applied to incomming connections.

Compare this to k8s, where an Ingress Controller ( F5 CC or NGINX controller) provides the referse proxy and the Ingress Resource defines the connection rules.

### Software Defined Network

### Source to Image (S2I)

A pipeline tool for producing images from source in a predicatable, repeatable way.

### Tools / Tooling



### WebConsole

