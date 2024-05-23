# Kustomize Generators

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/kustomizegen.jpg?raw=true" alt="kustomize_generators" width="300" height="300">
</div>

## Objective

Learn how to use Kustomize generators to create ConfigMaps and Secrets dynamically, ensuring flexible and reusable configurations for your Kubernetes resources.

## Prerequisites

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic knowledge of Kubernetes, YAML syntax, and Kustomize.

## Introduction

Welcome, noble custodian of the Openshift kingdom! Within the walls of your realm, ConfigMaps and Secrets serve as the magical artifacts that configure and secure your applications. Kustomize generators allow you to dynamically create these artifacts, ensuring that your configurations are flexible, reusable, and easily managed. Join us as we delve into the enchantment of Kustomize generators and enhance your dominion over the Openshift kingdom.

## Understanding Kustomize Generators

### The Magic of ConfigMap and Secret Generators

In the Openshift kingdom, Kustomize provides two powerful fields to generate ConfigMap and Secret resources: `configMapGenerator` and `secretGenerator`. These generators dynamically create configurations based on literals, files, or environment variables, allowing you to manage application settings and secrets efficiently.

In your kingdom, imagine ConfigMaps as enchanted scrolls containing vital information and Secrets as hidden treasures known only to trusted allies. Kustomize generators are the scribes and treasure keepers, ensuring that these scrolls and treasures are created and maintained seamlessly.

### Example of ConfigMap Generator

Consider the following example, where a `kustomization.yaml` file includes a `configMapGenerator`:

```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
namespace: my-app-stage
bases:
- ../../base
configMapGenerator:
- name: my-app-configmap
  literals:
    - msg="Hello!"
    - enable="true"
```

Executing the command `kubectl kustomize overlays/staging` will visualize a new ConfigMap, much like summoning a new enchanted scroll for your realm. Applying this configuration to the cluster ensures that the ConfigMap is incorporated into your Deployment:

```bash
kubectl apply -k overlays/staging
```

### Generating ConfigMaps with Different Methods

Kustomize allows multiple ways to populate the `configMapGenerator` field, including using files, environment files, or key-value pairs. These methods are akin to gathering knowledge from different tomes, scrolls, and sages within your kingdom.

#### Using Files

```yaml
configMapGenerator:
- name: configmap-1
  files:
    - application.properties
```

Example `application.properties` file:

```txt title="application.properties"
Day=Monday
Enable=True
```

#### Using Environment Files

```yaml
configMapGenerator:
- name: configmap-2
  envs:
    - configmap-2.env
```

Example `configmap-2.env` file:

```txt title="configmap-2.env"
Greet=Welcome
Enable=True
```

#### Using Literals

```yaml
configMapGenerator:
- name: configmap-3
  literals:
    - name="configmap-3"
    - description="literal key-value pair"
```

### Viewing Configurations

To view the details of resources and customizations defined by your `kustomization.yaml` file, use the following command:

```bash
kubectl kustomize <kustomization-directory>
```

For example:

```bash
kubectl kustomize .
```

This command is like unfurling a detailed map of your kingdom, revealing the locations of all enchanted scrolls and hidden treasures.

### Customizing Generator Behavior

The `generatorOptions` field allows you to alter the default behavior of Kustomize generators. This provides further flexibility in how ConfigMaps and Secrets are generated and managed, ensuring that your kingdom's needs are always met.

## Conclusion

Congratulations, wise steward of the Openshift kingdom! By mastering Kustomize generators, you can dynamically create ConfigMaps and Secrets, ensuring your applications are configured and secured with the utmost flexibility and efficiency. Just as a ruler adapts their strategies to the needs of the realm, you can now tailor your configurations to meet the demands of your environments. Embrace the power of Kustomize generators and fortify your Openshift domain with confidence.

With this newfound knowledge, you hold the keys to a well-organized and secure realm, where ConfigMaps and Secrets are generated with precision and ease. Your kingdom thrives under your vigilant guidance, as you skillfully wield the power of Kustomize to shape your domain.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>