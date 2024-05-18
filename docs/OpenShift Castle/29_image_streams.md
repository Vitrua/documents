# Image Streams

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/imagestreams.jpg?raw=true" alt="image_streams" width="300" height="300">
</div>

## Objective

Learn how to leverage image streams in Openshift to ensure reproducible, stable deployments of containerized applications and facilitate rollbacks.

## Prerequisites

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic knowledge of Openshift concepts and command-line interfaces (CLI).

## Introduction

Greetings, esteemed overseer of the Openshift kingdom! Within the fortress of your realm, image streams are the enchanted scrolls that guide your applications to stable and reproducible deployments. Unlike the upstream Kubernetes lands, where resources reference container images directly, Openshift resources reference these magical image streams. By mastering image streams, you ensure that your applications can be deployed reliably and rolled back to their last known-good state whenever needed. Join us as we uncover the secrets of image streams and enhance your dominion over the Openshift kingdom.

## Understanding Image Streams

### The Enchantment of Image Streams

In the mystical Openshift realm, image streams serve as a repository of container images, offering a stable, short name to reference these images, independent of registry servers and container runtime configurations. An image stream can reference multiple images from different registry servers and repositories, much like a library filled with books from various kingdoms, each tagged and cataloged for easy retrieval.

These image streams store metadata about their corresponding images, enabling quicker search and inspection without accessing the source registry server. Tags within image streams can even store image layers locally, acting as a cache and avoiding the need to fetch layers from external servers.

## Describing Image Streams

### Visualizing the Magic

To see the source image and current image ID for each image stream tag, use the `describe` command. This command is like opening a magical tome that reveals the secrets of your image streams:

```bash
oc describe is keycloak -n openshift
```

## Creating Image Streams and Tags

### Conjuring New Image Streams

You can create image streams in your project so that resources, such as Deployment objects, can use them. Here's how to create an image stream named "keycloak":

```bash
oc create is keycloak
```

After creating the image stream, use the `oc create istag` command to add image stream tags. This is like inscribing new spells in your book of magic. For example, add the 20.0 and 19.0 tags to the keycloak image stream:

```bash
oc create istag keycloak:20.0 --from-image quay.io/keycloak/keycloak:20.0.2
oc create istag keycloak:19.0 --from-image quay.io/keycloak/keycloak:19.0
```

To update an image stream tag with a new source image reference:

```bash
oc tag SOURCE-IMAGE IMAGE-STREAM-TAG
```

For example:

```bash
oc tag quay.io/keycloak/keycloak:20.0.3 keycloak:20.0
```

Use the `describe` command to verify the SHA ID of the new image to ensure the tag has been updated.

## Importing Image Stream Tags Periodically

### Automatic Updates with Scheduled Imports

To keep your image stream tags up to date automatically, Openshift can periodically check for new image versions and update the tags when a new version is detected. This ensures your magical defenses are always current. Activate this periodic refresh with the `--scheduled` option:

```bash
oc tag quay.io/keycloak/keycloak:20.0.3 keycloak:20.0 --scheduled
```

The default interval between verifications is 15 minutes.

## Configuring Image Pull-through

### Caching Images Locally

You can configure your image stream tags to cache the images in the Openshift internal container registry, ensuring quick access and reducing dependency on external sources. Use the `--reference-policy local` option:

```bash
oc tag quay.io/keycloak/keycloak:20.0.3 keycloak:20.0 --reference-policy local
```

## Using Image Streams in Deployments

### Enabling Local Lookup Policy

When creating a Deployment object, you can specify an image stream instead of a container image from a registry. Enable the local lookup policy with:

```bash
oc set image-lookup keycloak
```

Verify the policy with:

```bash
oc describe is keycloak
```

To retrieve the local lookup policy status for all image streams in the current project:

```bash
oc set image-lookup
```

To disable the local lookup policy:

```bash
oc set image-lookup keycloak --enabled=false
```

### Configuration in Deployments

You can configure a deployment to utilize an image stream by using the `--image` option when creating it:

```bash
oc create deployment mykeycloak --image keycloak:20.0
```

Openshift recognizes to look first for an image stream when a short name is used. This strategy ensures that your deployments are always using the most current and trusted images.

Image streams can also be used with other Kubernetes resources such as jobs, cronjobs, and pods.

## Conclusion

Embark on the journey of mastering image streams within the fortified bastion of Openshift. By understanding and implementing image streams, you ensure your applications are deployed reliably and can be easily rolled back to a stable state. Just as a wise ruler maintains a library of enchanted scrolls, you too can safeguard your applications and ensure their success within the Openshift kingdom.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>