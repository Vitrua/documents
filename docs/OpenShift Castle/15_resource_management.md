# Command Line Resources Management

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/declimper.jpg?raw=true" alt="command_line_management" width="300" height="300">
</div>

## Objective

Master the art of managing resources through command-line interfaces within the mystical confines of the Openshift castle, enabling efficient resource creation and configuration.

## Prerequisites

To embark on this journey of command-line resources management, you'll need:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic familiarity with command-line interfaces (CLI) and container concepts.

## Introduction

Welcome, traveler, to the wondrous realms of the Openshift castle, where digital landscapes intertwine with mystical energies. As we navigate the labyrinthine corridors of this ancient stronghold, we discover the need to manage resources with precision and efficiency. Here, amidst the ever-changing vistas of digital realms, lies the power of command-line tools to shape and mold the fabric of existence itself.

## Command Line Resources Management

### Imperative Commands: Crafting Realms with Swiftness

Imperative commands such as `create`, `set`, and `run` serve as the swift hand of creation within the castle's halls. They offer a rapid means of crafting pods and other resources, bypassing the need for intricate object definitions. Like skilled artisans, troubleshooters wield these commands to forge new realms with speed and agility.

#### Example Usage

```bash
oc run example-pod \
--image=docker.io/library/busybox \
--restart=Never \
-- echo "Hello, world!"
```

### Declarative Commands: Weaving Threads of Intention

Declarative commands beckon troubleshooters to weave threads of intention into the fabric of the digital tapestry. Through YAML files or templates, they define the desired state of resources, allowing for precise configuration and management. Within these commands lies the power to manifest visions into reality, shaping the very essence of the castle's domains.

#### Example Usage

```bash
oc new-app --template hello-world \
--param MESSAGE="Hello, world!"
```

### Workload Resources: Crafting Grand Designs

Workload resources such as Jobs, Deployments, and StatefulSets represent the grand designs within the castle's architecture. With commands like `oc create job`, troubleshooters breathe life into these constructs, imbuing them with purpose and function. Through these commands, they orchestrate the movements of digital legions, fulfilling the castle's ever-changing needs.

#### Example Usage

```bash
oc create job hello-job \
--image=docker.io/library/busybox \
-- /bin/echo "Hello, world!"
```

Embark on this grand journey of command-line resources management, as we navigate the enchanted pathways of creation and configuration within the mystical confines of the Openshift castle.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>
