# Secrets & Configmaps

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/secret.jpg?raw=true" alt="secrets_configmaps" width="300" height="300">
</div>

## Objective

Learn how to create secrets and configmaps, to inject as volumes, and manipulate them to securely store sensitive information and configuration data.

## Prerequisites

To embark on this journey of fortifying the bastion, you'll need:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic understanding of Openshift concepts and command-line interfaces (CLI).

## Introduction

Welcome, guardian of secrets, to the realm of fortifying the bastion within the enchanted confines of Openshift. Just as a fortress requires secure storage for its most sensitive information and precise configuration for its inner workings, so too must your applications be fortified with secrets and configmaps. Join us as we delve into the art of safeguarding your fortress and ensuring its resilience against digital adversaries.

## Creating Secrets and Configmaps

### Crafting Shields and Scrolls

In Openshift, troubleshooters can create secrets and configmaps to fortify the bastion of their fortress. Secrets provide a secure means of storing sensitive information such as passwords, API tokens, and certificates, while configmaps hold configuration data in the form of key-value pairs.

### Example Usage

```bash
oc create secret generic <secret_name> \
--from-literal <key1>=<secret1> \
--from-literal <key2>=<secret2>

oc create secret tls <secret_tls_name> \
--cert /<path-to-certificate> --key /<path-to-key>

oc create cm <configmap_name> \
--from-literal <key1>=<config1> --from-literal <key2>=<config2>
```

These commands populate the 'create' command with the necessary files or key-value pairs, similar to the 'kubectl' command, enabling troubleshooters to fortify their fortress with shields and scrolls of secrecy and configuration. Mind as usual, that data created in this way are not encrypted, an expert thief would be able to retrieve them.

You can apply these configurations in a declarative way too, utilizing the yaml scrolls, and remember to inject them in the corresponding deployment to make them active.

## Secrets and Configmaps as Volumes

### Unveiling Hidden Treasures

In the realm of Openshift, intrepid explorers can bind secrets and configmaps to directories within their fortress's chambers. By doing so, they allow their applications to access the secrets and configuration data securely, akin to uncovering hidden treasures within the labyrinthine corridors of their bastion.

### Example Usage

```bash
oc set volume deployment/my-app --add --type secret --secret-name my-app-secret --mount-path /app-secrets
```

With this command, troubleshooters can mount the created secrets to an '/app-secrets' directory within the pod, granting their applications access to the concealed knowledge securely.

To confirm the attachment of the volume to the deployment, one may invoke:

```bash
oc set volume deployment/my-app
```

Furthermore, to seamlessly integrate these treasures into the fabric of your applications, you can set environment variables from the secrets and configmaps. For instance:

```bash
oc set env deployment/my-app \
--from secret/my-app-secret --prefix MYSQL_
```

This command augments the application's environment variables with the key-value pairs from the secrets, enabling seamless interaction with the concealed knowledge within the fortress.

## Updating and Deleting Secrets & Configmaps

### Manipulating the Threads of Fate

In the labyrinthine corridors of Openshift, troubleshooters can manipulate the threads of fate that bind secrets and configmaps to their fortress's essence. By deftly updating and deleting these artifacts, they ensure the resilience and security of their bastion's secrets and configurations.

### Example Usage

To update secrets and configmaps from the command line, troubleshooters embark on a two-step journey of visualization and effective modification. For instance:

```bash
oc extract secret/my-app-secrets -n demo --to /tmp/my-app --confirm
oc set data secret/my-app-secrets -n demo --from-file /tmp/my-app/root_password
```

These commands allow troubleshooters to visualize and locally edit the secrets and configmaps before effecting the update, ensuring precision and accuracy in their modifications. After updating, it's essential to restart the pods to ensure they read the updated values, unless they are mounted as volumes and the software doesn't read the configuration data only at startup time.

For secrets and configmaps that have outlived their purpose and are no longer needed, troubleshooters can invoke the 'delete' command, liberating their fortress from the burdens of obsolete artifacts. For example:

```bash
kubectl delete secret/my-app-secrets -n demo
oc delete configmap/my-app-map -n demo
```

With these commands, troubleshooters can seamlessly update and delete secrets and configmaps, maintaining the sanctity and security of their fortress within the mystical confines of Openshift.

## Conclusion 
Fortify your bastion and safeguard your fortress against the machinations of digital adversaries within the mystical confines of Openshift.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>
