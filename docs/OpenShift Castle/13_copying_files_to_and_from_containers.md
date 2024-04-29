# Copying Files to and from Containers

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/twins.jpg?raw=true" alt="copying_files" width="300" height="300">
</div>

## Objective

Master the art of copying files to and from containers within the mystical confines of the Openshift castle, enabling seamless data exchange between realms.

## Prerequisites

To embark on this journey of file manipulation and synchronization, you'll need:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic familiarity with command-line interfaces (CLI) and container concepts.

## Introduction

As we navigate the ethereal landscapes of the Openshift castle, the need to exchange files with containers becomes apparent. Here, amidst the shimmering data streams, lies the ability to synchronize files between realms, enabling seamless interaction and data exchange.

## Copying Files to and from Containers

### Using the `oc cp` Command

To copy files to and from containers using the `oc cp` command, the `tar` binary must be present in the container. This command allows troubleshooters to exchange files between local directories and containers with ease:

- `oc cp <SOURCE> <DEST>`: Copy files from a running container to a local directory, or from a local directory to a running container.

#### Example Usage

```bash
oc cp my-app-pod:/opt/app/config.ini /tmp/config.ini
oc cp /tmp/config.ini my-app-pod:/opt/app/
```

### Synchronizing Files with `oc rsync`

For directory synchronization between a local directory and a directory within a container, troubleshooters can utilize the `oc rsync` command:

- `oc rsync <SOURCE> <DEST>`: Synchronize files and directories between a local directory and a directory within a container.

#### Example Usage

```bash
oc rsync my-app-pod:/var/www/ /tmp/web_files
```

### Notes

- When targeting a file path within a pod for either the SOURCE or DEST argument, use the `<pod_name>:<path>` format, and optionally include the `-c <container_name>` option for specifying a particular container within a pod.

Embark on this journey of file manipulation and synchronization, as we facilitate seamless data exchange between realms within the enchanted confines of the Openshift castle.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>
