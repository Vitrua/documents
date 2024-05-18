# StatefulSet Configuration

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/persistentstorage.jpg?raw=true" alt="storage_classes" width="300" height="300">
</div>

## Objective

Configure StatefulSets effectively in your Kubernetes cluster.

## Prerequisites

- Access to a Kubernetes cluster or a terminal emulator connected to one.
- Basic knowledge of Kubernetes concepts and command-line interfaces (CLI).

## Introduction

In the dynamic landscape of Kubernetes, most applications are designed to be stateless, akin to agile warriors traversing the castle's battlements. However, certain applications, such as databases, require persistent storage and consistent identities across pod restarts. StatefulSets serve as the stout walls and sturdy gates of the castle, providing the necessary mechanisms to manage such stateful applications within Kubernetes clusters.

## StatefulSet Configuration: Building the Castle's Keep

### Understanding Stateful Components

StatefulSets enable the deployment of stateful applications by providing ordered pod creation, stable network identifiers, and unique persistent storage for each pod instance. This ensures that each pod in the StatefulSet maintains a consistent identity across restarts and rescheduling, much like the steadfast guards stationed atop the castle's towers.

#### Example Manifest: Fortifying the Castle Walls

```yaml title="mysql-server.statefulset.yaml"
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mysql-server
spec:
  selector:
    matchLabels:
      app: database
  replicas: 3
  template:
    metadata:
      labels:
        app: database
    spec:
      containers:
      - env:
        - name: MYSQL_USER
          valueFrom:
            secretKeyRef:
              key: user
              name: db-credentials
        image: mysql/mysql-server:8.0
        name: database
        ports:
        - containerPort: 3306
          name: database
        volumeMounts:
        - mountPath: /var/lib/mysql
          name: data
      terminationGracePeriodSeconds: 10
  volumeClaimTemplates:
  - metadata:
      name: data
    spec:
      accessModes: [ "ReadWriteOnce" ]
      storageClassName: "example-storage-class"
      resources:
        requests:
          storage: 2Gi
```

In this manifest, we erect the castle's keep, naming it "mysql-server" with three replicas. Each replica houses a pod with a MySQL database container, fortified with persistent storage for data persistence. The `volumeClaimTemplates` section outlines the blueprint for the persistent volume claim (PVC) used by each pod instance, ensuring the castle's storerooms remain well-stocked and impregnable.

### Managing StatefulSets: Protecting the Castle's Integrity

StatefulSets, akin to the castle's ramparts and battlements, demand careful management to uphold the fortress's integrity and resilience. Let us explore how to safeguard and fortify our castle against potential threats.

#### Creating a StatefulSet: Raising the Castle's Walls

To raise the castle's walls, apply the manifest file using the `kubectl create` command:

```bash
kubectl create -f <stateful_manifest_name>
```
For instance:
```bash
kubectl create -f mysql-server.statefulset.yaml
```

#### Updating a StatefulSet: Reinforcing the Castle's Defenses

To reinforce the castle's defenses, edit the manifest file accordingly and apply the changes using `kubectl apply`:

```bash
kubectl apply -f <stateful_manifest_name>
```
For example:
```bash
kubectl apply -f updated-mysql-server.statefulset.yaml
```

#### Deleting a StatefulSet: Securing the Castle Gates

To secure the castle gates and dismantle any potential threats, use the `kubectl delete` command:

```bash
kubectl delete statefulset <statefulset_name>
```
For instance:
```bash
kubectl delete statefulset mysql-server
```

## Conclusion

StatefulSets serve as the bastions of fortitude within Kubernetes clusters, safeguarding stateful applications with unwavering resilience. By mastering their configuration and management principles, you can fortify the castle of your Kubernetes realm, ensuring the perpetuity and security of your data with the stalwart vigilance of its guardians.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>