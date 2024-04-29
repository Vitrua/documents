# OC Images

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/ocimages.jpg?raw=true" alt="oc_images" width="300" height="300">
</div>

## Objective

Manage container images with the `oc image` command.

## Prerequisites

To embark on this journey of exploration and enlightenment, you'll need:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic familiarity with command-line interfaces (CLI) and container concepts.

## Introduction

As we navigate the intricate pathways of the Openshift castle, we encounter the realm of container images, governed by the mystical `oc image` command. Here, amidst the shimmering data streams, lies the essence of containerization waiting to be unveiled.

## Exploring OC Images

### Commanding the Digital Realms

The `oc image` command serves as the wielder's tool to inspect, configure, and retrieve information about container images within the castle's domain.

### Mystical Options at Your Command

Behold the commands bestowed upon the keeper of this arcane tool:

- `oc image info`: Gather insights into the properties and configurations of container images. Utilize options like `--filter-by-os` to manage specific types of images, e.g.:
    ```bash
    oc image info docker.io/ibmcom/ibm-cloud-databases-redis-catalog --filter-by-os amd64
    ```

More powers can be:

- `oc image append`: Add layers to container images, empowering them with additional capabilities before pushing them to a registry.

- `oc image extract`: Retrieve or copy files from container images to a local disk, without the need to run the image as a container.

- `oc image mirror`: Facilitate the copying or mirroring of container images between different registries or repositories, enabling seamless transfers and management.

### Journey Deeper into the Digital Realms

With `oc image` as your guide, embark on a journey deeper into the digital realms of containerization, unlocking the hidden potential within container images and harnessing their power for your endeavors within the castle.

Embark on this journey of discovery, as we unravel the mysteries of OC Images within the enchanted confines of the Openshift castle.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>
