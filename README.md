# k8s
Kubernetes/Helm configs for ReportPortal

**Do note that this is a Beta version**


This Helm project is created to setup ReportPortal with only one commando.  
The help chart is tested on AWS Kubernetes Production Cluster and creates a fully working ReportPortal project

The chart installs all mandatory services to run ReportPortal

The Helm chart installation consist of the following .yaml files:

- Statefulset and Service files of: `Analyzer, Api, Elasticsearch, Gateway, Index, Mongodb, Registry, UAT, UI` that are used for deployment and communication between services.
- PersistentVolume files: `Elasticsearch, Mongodb, Registry`
- A `Ingress` to access the UI
- A `values.yaml` which exposes a few of the configuration options in the
charts.
- A `templates/_helpers.tpl` file which contains helper templates. 

### Instaling Helm on your k8s cluster manager 
```console
$ curl -fsSL https://raw.githubusercontent.com/fishworks/gofish/master/scripts/install.sh | bash
$ gofish init
$ gofish install helm
$ helm init
```

###  Create a namespace
```console
$ kubectl create ns reportportal
```

###  Creating an EBS volume on AWS using cli
It's for elasticsearch PV
```console
aws ec2 --profile ti create-volume --size 80 --region us-east-1 --availability-zone us-east-1a
```
It's for elasticsearch PV
```console
aws ec2 --profile ti create-volume --size 75 --region us-east-1 --availability-zone us-east-1a
```
It's for elasticsearch PV
```console
aws ec2 --profile ti create-volume --size 50 --region us-east-1 --availability-zone us-east-1a
```

### Clone and deploy ReportPortal Project
```console
$ git clone https://github.com/richardsonlima/k8s.git
$ cd k8s 
$ helm install . 
```

**Tip:** View all

Take a look on it and access `reportportal` using Ingress (AWS ELB) Adress over port 9999 on your browser
```console 
$ kubectl --namespace=reportportal describe svc/gateway|grep 'LoadBalancer Ingress'
```
