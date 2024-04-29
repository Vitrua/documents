# Editing Resources

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/manipulation.jpg?raw=true" alt="editing_resources" width="300" height="300">
</div>

## Objective

Learn the art of editing resources within the mystical confines of the Openshift castle, wielding the power to shape and mold configurations with finesse.

## Prerequisites

To embark on this journey of editing and transformation, you'll need:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic familiarity with command-line interfaces (CLI) and container concepts.

## Introduction

As we delve deeper into the enchanted realms of the Openshift castle, the need to make changes to resources arises. Here, amidst the flux of digital energies, lies the ability to edit configurations and orchestrate transformations.

## Editing Resources

### Direct Manipulation of Configurations

After the initial phase of inspection and data gathering, troubleshooters can directly test and apply changes to running containers using commands like `oc edit` and `oc patch`:

- `oc edit`: Open the resource configuration in an editor, allowing for direct modification of parameters and settings.
- `oc patch`: Apply changes to resource configurations using JSON or YAML patches, enabling precise alterations with surgical precision.

#### Example Usage

```bash
oc edit pod my-app-pod

oc patch pod valid-pod --type='json' \
-p='[{"op": "replace", "path": "/spec/containers/0/image", \
"value":"docker.io/my-new-image:latest"}]'
```

### Port Forwarding for Investigation

For temporary port forwarding to expose connectivity to a pod for investigation purposes, troubleshooters can utilize the `oc port-forward` command:

- `oc port-forward <RESOURCE> <EXTERNAL_PORT:CONTAINER_PORT>`: Establish a temporary connection between a local port and a container port, facilitating investigation and analysis.

#### Example Usage

```bash
oc port-forward nginx-app-ab12c 8080:80
```

Embark on this journey of editing and transformation, as we wield the power to shape the digital realms within the enchanted confines of the Openshift castle.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>
