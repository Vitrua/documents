# Deleting Resources

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/deleter.jpg?raw=true" alt="delete_resources" width="300" height="300">
</div>

## Objective

Master the art of deleting resources within the confines of the Openshift castle, ensuring cleanliness and efficiency in your digital domains.

## Prerequisites

To embark on this journey of resource deletion and management, you'll need:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic familiarity with command-line interfaces (CLI) and Kubernetes concepts.

## Introduction

As we navigate the corridors of the Openshift castle, we encounter the necessity of resource deletion. Here, amidst the constant ebb and flow of digital entities, lies the art of tidying and organization.

## Deleting Resources

Resources within the castle can be removed with the `delete` command, wielded with precision and care:
```bash
oc delete pod my-app [options]
```
Options abound to tailor the deletion process to your specific needs:

- `-l <key:value>`: Selects resources based on the inserted label key:value.
- `-f <file_path>`: Deletes resources specified in a file, providing the full path for accuracy.
- `--grace-period=`: Specifies the seconds before a pod is forcibly terminated.
- `--now`: Sets the grace period to 1 second, immediately shutting down the pod.
- `--force`: Forcibly deletes the pod, overriding any constraints.
- `--all`: Deletes all pods within a project, ensuring a clean slate for future endeavors.

## Full Project Deletion

For larger-scale deletions, entire projects and their associated resources can be removed with a single command:
```bash
oc delete project <project_name>
```

Embark on this journey of resource management, as we wield the power of deletion within the hallowed halls of the Openshift castles.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>