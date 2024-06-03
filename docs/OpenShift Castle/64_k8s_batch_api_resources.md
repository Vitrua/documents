# Kubernetes Batch API Resources

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/batchapi.jpg?raw=true" alt="batchapi" width="300" height="300">
</div>

## Objective

This tutorial aims to guide you through the process of automating tasks in OpenShift using Kubernetes jobs and cron jobs.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Familiarity with Kubernetes batch resources, including jobs and cron jobs.
- Basic knowledge of YAML syntax for creating and editing configuration files.

## Introduction

In the grand kingdom of OpenShift, automation plays a crucial role in maintaining order and efficiency. Just as a medieval castle relies on automated mechanisms like clock chimes and automated gates, OpenShift uses Kubernetes batch resources—jobs and cron jobs—to manage repetitive and scheduled tasks. These tasks range from simple one-off commands to complex maintenance routines that keep the infrastructure running smoothly. Understanding how to effectively utilize these batch resources is key to ensuring the kingdom's stability and prosperity.

## Kubernetes Jobs

A Kubernetes job is akin to a knight given a specific quest to complete a single task. It ensures that a specified number of pods run to completion successfully. The job resource includes a pod template that describes the task to execute.

### Example:

To create a job, you can use the `oc create job --dry-run=client` command to generate the YAML representation, like a scribe drafting the quest details for the knight:

```bash
oc create job --dry-run=client -o yaml test \
--image=registry.access.redhat.com/ubi9/ubi:9.4 \
-- curl https://example.com
```

This command outlines a job that uses a pod with a container running the Universal Base Image (UBI) and executes a curl command to access a website.

## Kubernetes Cron Jobs

A Kubernetes cron job is like a castle bell ringer, tasked with ringing the bell at specific times. It runs jobs on a schedule, ensuring that tasks are performed regularly.

### Example:

To create a cron job, you can use the `oc create cronjob --dry-run=client` command to get the YAML representation:

```bash
oc create cronjob --dry-run=client -o yaml test \
--image=registry.access.redhat.com/ubi9/ubi:9.4 \
--schedule='0 0 * * *' \
-- curl https://example.com
```

This command creates a cron job scheduled to run at midnight every day, executing a curl command using a container running the UBI.

## Automating Application Maintenance Tasks

Just as the castle has regular maintenance to keep its structures sound, applications in OpenShift often need regular maintenance tasks. Here’s an example of a cron job automating a WordPress backup:

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: wordpress-backup
spec:
  schedule: 0 2 * * 7
  jobTemplate:
    spec:
      template:
        spec:
          dnsPolicy: ClusterFirst
          restartPolicy: Never
          containers:
          - name: wp-cli
            image: registry.io/wp-maintenance/wp-cli:2.7
            resources: {}
            command:
            - bash
            - -xc
            args:
            - >
              wp maintenance-mode activate ;
              wp db export | gzip > database.sql.gz ;
              wp maintenance-mode deactivate ;
              rclone copy database.sql.gz s3://bucket/backups/ ;
              rm -v database.sql.gz ;
```

This cron job activates WordPress maintenance mode, exports and compresses the database, uploads it to an S3 bucket, and then cleans up.

## Automating Cluster Maintenance Tasks

Just as the castle's guards perform regular patrols to ensure safety, clusters need regular maintenance to stay healthy. Here’s an example of a script for image pruning:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: maintenance
  app: crictl
data:
  maintenance.sh: |
    #!/bin/bash
    NODES=$(oc get nodes -o=name)
    for NODE in ${NODES}
    do
      echo ${NODE}
      oc debug ${NODE} -- \
      chroot /host \
        /bin/bash -xc 'crictl images ; crictl rmi --prune'
      echo $?
    done
```

This script lists and prunes unused images on each node. It can be executed as a cron job:

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: image-pruner
spec:
  schedule: 0 * * * *
  jobTemplate:
    spec:
      template:
        spec:
          dnsPolicy: ClusterFirst
          restartPolicy: Never
          containers:
          - name: image-pruner
            image: quay.io/openshift/origin-cli:4.12
            resources: {}
            command:
            - /opt/scripts/maintenance.sh
            volumeMounts:
            - name: scripts
              mountPath: /opt
          volumes:
          - name: scripts
            configMap:
              name: maintenance
              defaultMode: 0555
```

## Assigning Privileged Access

Sometimes, maintenance tasks require higher privileges, much like how certain castle tasks require special keys. You can create a service account with the required privileges and associate it with the cron job:

```bash
oc create serviceaccount maintenance-sa
oc adm policy add-scc-to-user privileged -z maintenance-sa
```

Then, specify the service account in the cron job:

```yaml
spec:
  serviceAccountName: maintenance-sa
```

## Conclusion

By leveraging Kubernetes jobs and cron jobs, you can automate and schedule critical tasks in OpenShift, ensuring your applications and clusters are well-maintained. This automation is akin to the efficient operation of a castle, where every task is carefully scheduled and executed, ensuring the kingdom runs smoothly and securely.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>