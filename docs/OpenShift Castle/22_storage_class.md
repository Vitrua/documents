# Storage Classes

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/storageclasses.jpg?raw=true" alt="storage_classes" width="300" height="300">
</div>

## Objective

Delve into the realm of storage classes within Openshift, understanding how they define the characteristics and capabilities of persistent storage for your applications.

## Prerequisites

Before embarking on this journey of storage classes, ensure you possess:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Familiarity with basic Openshift concepts and command-line interfaces (CLI).

## Introduction

Welcome, architect of storage, to the realm of storage classes within the fortified bastion of Openshift. As the weaver of storage destinies, you possess the power to define the characteristics and capabilities of persistent storage within your fortress. Join us as we unravel the mysteries of crafting and managing storage classes, empowering your applications with tailored storage solutions within the mystical confines of Openshift.

## Defining Storage Classes

### Crafting the Blueprint of Destiny

In the tapestry of persistent storage, storage classes serve as the blueprint of destiny, defining the characteristics and capabilities of persistent volumes (PVs). Through declarative means, troubleshooters manifest the essence of their storage solutions, specifying parameters such as storage provider, volume type, and reclaim policy.

#### Example Usage

To craft a storage class, troubleshooters wield the power of YAML manifests, defining the blueprint of destiny within their fortress. For example:

```yaml title="io1-gold-storage.yaml"
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: io1-gold-storage
  annotations:
    storageclass.kubernetes.io/is-default-class: 'false'
    description: 'Provides RWO and RWOP Filesystem & Block volumes'
parameters:
  type: io1
  iopsPerGB: "10"
provisioner: kubernetes.io/aws-ebs
reclaimPolicy: Delete
volumeBindingMode: Immediate
allowVolumeExpansion: true
```

With this manifest, troubleshooters define a storage class named "io1-gold-storage", specifying parameters such as storage type, IOPS per GB, provisioner, and reclaim policy. They can then create the storage class using the command:

```bash
oc create -f io1-gold-storage.yaml
```

## Conclusion

Embark on this journey of crafting storage destinies within the fortified bastion of Openshift. By mastering the art of storage classes, you empower your applications with tailored storage solutions, ensuring their resilience and efficiency within the mystical confines of Openshift.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>