# Persistent Storage

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/storage.jpg?raw=true" alt="persistent_storage" width="300" height="300">
</div>

## Objective

Master the realm of persistent storage within Openshift, enabling your applications to retain critical data across time and space.

## Prerequisites

Before delving into the depths of persistent storage, ensure you possess:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Familiarity with basic Openshift concepts and command-line interfaces (CLI).

## Introduction

Welcome, custodian of continuity, to the arcane realm of persistent storage within the fortified bastion of Openshift. As the guardian of data across the ebb and flow of time, you possess the power to shape the very essence of continuity within your fortress. Join us as we unravel the mysteries of creating and managing persistent volumes, ensuring the perpetuity of your fortress's data within the mystical confines of Openshift.

## Creating Persistent Volumes (PVs)

### Forging the Chains of Continuity

In the realm of Openshift, troubleshooters can forge the chains of continuity by creating persistent volumes (PVs) through declarative means. Utilizing YAML manifests, they define the characteristics of the PV, such as capacity, access modes, and storage classes.

#### Example Usage

To create a Persistent Volume, troubleshooters can wield the power of YAML manifests, crafting the essence of continuity within their fortress. For instance:

```yaml title="my-app.pv.yaml"
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-app-pv
spec:
  capacity:
    storage: 20Gi
  accessModes:
    - ReadWriteOnce
  volumeMode: Block
  persistentVolumeReclaimPolicy: Retain
  fc:
    targetWWNs: ["12345a1234567bcd1"]
    lun: 0
    readOnly: false
```

With this manifest, troubleshooters define a Persistent Volume named "my-app-pv" with a capacity of 20Gi, accessible in ReadWriteOnce mode. They can then create the PV using the command:

```bash
oc create -f my-app.pv.yaml
```

## Claiming Persistent Volume Storage (PVC)

### Embracing the Threads of Destiny

Once the PV is forged, troubleshooters can embrace the threads of destiny by claiming its storage through Persistent Volume Claims (PVCs). By specifying the desired characteristics such as capacity and access mode, they bind the PV to their application's essence, ensuring continuity and resilience.

#### Example Usage

To claim persistent volume storage, troubleshooters manifest the essence of their destiny within the PVC. For example:

```yaml title="my-app.pvc.yaml"
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-app-pvc
  labels:
    app: my-app
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 15Gi
```

With this manifest, troubleshooters define a PVC named "my-app-pvc" requesting 15Gi of storage in ReadWriteOnce mode. They can then generate the PVC using the command:

```bash
oc create -f my-app.pvc.yaml
```

## Managing Persistent Volumes in Deployments

### Weaving Destiny into the Fabric of Applications

With the PVs and PVCs crafted, troubleshooters can weave the threads of destiny into the fabric of their applications by mounting the PVCs within their deployments. Utilizing the 'set volumes' command, they bind the PVC to the desired mount path within the deployment, ensuring seamless interaction between the application and its persistent storage.

#### Example Usage

To mount PVCs within deployments, troubleshooters invoke the 'set volumes' command, integrating destiny into the fabric of their applications. For instance:

```bash
oc set volumes deployment/my-app \
--add \
--name my-app-pv \
--type persistentVolumeClaim \
--claim-mode rwo \
--claim-size 15Gi \
--mount-path /var/lib/my-app \
--claim-name my-app-pvc
```

## Managing Persistent Volumes

### Ensuring the Continuity of Destiny

In the ever-evolving saga of your fortress's destiny, troubleshooters must master the art of managing persistent volumes. From retrieval to deletion, they must ensure the continuity and resilience of their fortress's data across time and space.

#### Retrieving Persistent Volumes

Troubleshooters can retrieve information about persistent volumes using the 'get' command. For instance:

```bash
oc get pv
```

This command provides an overview of all persistent volumes within the Openshift cluster, enabling troubleshooters to monitor and manage their fortress's storage resources.

#### Deleting Persistent Volumes

In the cycle of renewal and rebirth, troubleshooters must sometimes release the shackles of the past by deleting persistent volumes that have outlived their purpose. Deleting a PV is a multi-step process that involves careful consideration and execution to ensure the continuity and resilience of the fortress's data.

##### Step 1: Delete the PVC

Before deleting a PV, troubleshooters must first delete the associated PVC to release the claim on the volume. For example:

```bash
oc delete pvc my-app-pvc
```

This command frees the PVC named "my-app-pvc" from the confines of the fortress, preparing the PV for deletion.

##### Step 2: Delete the PV

Once the PVC is deleted, troubleshooters can proceed to delete the PV using the 'delete' command. For example:

```bash
oc delete pv my-app-pv
```

This command releases the persistent volume named "my-app-pv" from the Openshift cluster, ensuring the continuity and resilience of the fortress's storage resources.

## Conclusion

Embark on this journey of continuity and resilience within the fortified bastion of Openshift. By mastering the art of persistent storage, you ensure the perpetuity of your fortress's data, safeguarding it against the ravages of time and entropy.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>
