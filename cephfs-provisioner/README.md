# cephfs-provisioner

[cephfs-provisioner](https://github.com/kubernetes-incubator/external-storage/tree/master/ceph/cephfs) is a Kubernetes Storage provider that makes you able to create cephfs volume claims.
To use, add the `provisioner: ceph.com/cephfs` to your StorageClass resource

## TL;DR;
```
$ helm install cephfs-provisioner
```

## Introduction
This charts bootstraps a cephfs-provisioner deployment on a Kubernetes cluster using the Helm package manager.

## Prerequisites
- Kubernetes 1.10+

## Installing the Chart
To install the chart with the release name my-release:
```
$ helm install --name my-release cephfs-provisioner/
```
This command deploys cephfs-provisioner on the Kubernets cluster in the default configuration. The [configuration](#configuration) lists the parameters that can be configured during installation.

## Uninstallting the Chart
To install/delete the `my-release` deployment:
```
$ hem delete my-release
```
This command removes all Kubernetes components associated wit hthe chart and deletes the release

## Configuration
The following table lists the configuration parameters of the cephfs-provisioner chart and their default values.

Parameter | Description | Default
--- | --- | ---
`replicaCount` | desired number of provisioner pods | `1`
`namespace` | namespace of deployment | `cephfs`
`image.repository` |  cephfs-provisioner container image repository | `quay.io/external_storage/cephfs-provisioner`
`image.tag` | container image tag | `v2.1.0-k8s1.11`
`image.pullPolicy` | container pull policy | `IfNotPresent`
`resources` | provisioner pod resource requests & limits | <code> requests: <br>&nbsp;cpu: 100m<br>&nbsp;memory: 128Mi<br>limits:<br>&nbsp;cpu: 200m<br>&nbsp;memory: 256Mi</code>

```
$ helm install cephfs-provisioner --name my-release \
    --set namespace=cephfs-namespace
```
Alternatively, a YAML file that specifies the values for the paramters can be provided while installing the chart:
```
$ helm install cephfs-provisioner --name my-release -f values.yaml
```

## Using the cephfs-provisioner

After installing this helm chart you can create a StorageClass which makes use of the provisioner `ceph.com/cephfs`. After StorageClass is deployed to your Kubernetes cluster a PersistentVolumeClaim can be deployed using the CephFS StorageClass. Finally make use of the PeristentVolumeClaim in the deployment of your app.

