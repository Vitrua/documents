# Pods Creation and Management

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/createpod.jpg?raw=true" alt="pods_creation" width="300" height="300">
</div>

## Objective

Learn the art of creating and managing pods within the bastion of the Openshift citadel, laying the groundwork for your digital domains.

## Prerequisites

To embark on this journey of creation and mastery, you'll need:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic familiarity with command-line interfaces (CLI) and Kubernetes concepts.

## Introduction

As we lay the cornerstone of our digital domains within the fortified confines of the Openshift citadel, we delve into the realm of pod creation and management. Here, amidst the hum of activity, like the rooms of a castle, lies the little foundations upon which our containerized realms shall thrive.

## Pods Creation

The creation of pods, the very crucible of containerization, is an art mastered through the commands of 'kubectl' or 'oc CLI'. With the `run` command, we breathe life into our digital entities:
```bash
oc run <RESOURCE/NAME> --image <IMAGE> [options]
oc run <RESOURCE/NAME> --image <IMAGE> --command -- cmd <arg1 ... argN>
```
To commence an interactive session within the pod's container, the `-it` option is invoked:
```bash
oc run -it my-app --image docker.io/library/busybox --command -- /bin/bash
```
Further options allow for fine-tuning the creation process, specifying restart policies, environment variables, and automatic deletion after the session's conclusion:
```bash
kubectl run -it my-app --rm --image docker.io/library/busybox --env MY_PASSWORD=P455w@rd --restart Never --command -- date
```
In the realm of Openshift, containers created by regular users are subject to the constraints imposed by the Security Context Constraints controller, ensuring a safe environment.

## Executing commands in running pod

When a pod is already in motion, commands can still be executed within its confines using `exec`:
```bash
oc exec <RESOURCE/NAME> -- <COMMAND> [args...] [options]
```
For an interactive session, the `-i` and `-t` flags once again guide our path. In multi-container pods, the `-c` or `--container=` flag designates the specific container for command execution.

Embark on this journey of creation and management, as we forge the foundations of our digital realms within the hallowed halls of the Openshift citadel.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>