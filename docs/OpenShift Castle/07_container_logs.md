# Explore Container Logs

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/explorepod.jpg?raw=true" alt="container_logs" width="300" height="300">
</div>

## Objective

Uncover the secrets held within the logs of containers, shedding light on the activities and events transpiring within the walls of the Openshift citadel.

## Prerequisites

To embark on this journey of exploration and revelation, you'll need:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic familiarity with command-line interfaces (CLI) and Kubernetes concepts.

## Introduction

As we delve into the depths of the Openshift citadel, we turn our attention to the archives of container logs. Here, amidst the echoes of past events, lies a wealth of information waiting to be discovered and deciphered.

## Container Logs

The logs of a container, akin to the chronicles of history, provide insights into the activities and events within. To retrieve these logs, adventurers employ the following command with various options:
```bash
oc logs <pod_name> [options]
```
- `-l` or `--selector=''`: Filters objects based on label key:value constraint.
- `--tail=`: Specifies the number of lines of logs to display.
- `-c` or `--container=`: Useful when multiple containers exist in a pod.
- `-f` or `--follow=`: Streams logs for a container.
- `-p` or `--previous=true`: Prints logs for a previous container instance in the pod, if available.

## Attach to Pods
For a more immersive experience, the `attach` command allows adventurers to connect to and start an interactive session on a running container within a pod:
```bash
oc attach my-app -it
```

Embark on this journey of exploration and revelation, as we illuminate the archives of the Openshift citadel and uncover the secrets hidden within its container logs.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>