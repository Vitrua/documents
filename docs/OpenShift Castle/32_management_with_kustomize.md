# Manage resources with Kustomize

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/kustomize.jpg?raw=true" alt="kustomize" width="300" height="300">
</div>

## Objective

Learn how to use Kustomize to manage Kubernetes configurations, enabling declarative changes while preserving the original base YAML files.

## Prerequisites

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic knowledge of Kubernetes and YAML syntax.

## Introduction

Welcome, master architect of the Openshift kingdom! Just as a wise ruler uses blueprints to design and modify their castle, Kustomize is a powerful tool that helps you manage and adapt your Kubernetes configurations. By grouping your resources into directories and utilizing Kustomize's capabilities, you can easily customize configurations for different environments while preserving the integrity of your original files. Join us as we explore the magical world of Kustomize and enhance your ability to manage the Openshift realm.

## Understanding Kustomize

### The Magic of Kustomize

In the Openshift kingdom, Kustomize acts like a master builder’s toolkit. It allows you to group Kubernetes resources in a directory, make declarative changes, and adapt these resources for various environments and clusters. Kustomize works on directories containing a `kustomization.yaml` file at the root, with the concepts of *base* and *overlays* guiding your modifications.

### Customizing for Multiple Environments

Kustomize enables you to customize configurations for multiple environments using *overlays* and *patching*. This mechanism has two elements: *patch* and *target*. A patch specifies the changes to be made, while the target defines the specific resource to be modified.

### Example of Patching

Consider the following example, where a `kustomization.yaml` file is used to apply patches directly within the file:

```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
namespace: stage-environment
patches:
- patch: |-
    - op: replace
    path: /metadata/name
    value: my-app-stage
  target:
    kind: Deployment
    name: my-app
- patch: |-
    - op: replace
    path: /spec/replicas
    value: 15
  target:
    kind: Deployment
    name: my-app
bases:
- ../../base
commonLabels:
  env: stage
```

Alternatively, you can use a separate patch file:

```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
namespace: prod-environment
patches:
- path: patch.yaml
  target:
    kind: Deployment
    name: my-app
  options:
    allowNameChange: true
bases:
- ../../base
commonLabels:
  env: prod
```

Where the `patch.yaml` file contains:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-prod
spec:
  replicas: 5
```

## View, Deploy, and Delete Resources Using Kustomize

### Rendering Manifests

To render the manifests without applying them to the cluster, use the `kubectl kustomize` command. This is like previewing the blueprints before constructing the castle:

```bash
kubectl kustomize <kustomization-directory>
```

For example:

```bash
kubectl kustomize overlay/production
```

### Applying Kustomizations

To apply the kustomization to the cluster, use the `-k` flag with `kubectl apply`. This is akin to putting the castle blueprints into action:

```bash
kubectl apply -k overlay/production
```

### Deleting Resources

To remove resources deployed using Kustomize, use the `-k` flag with the `oc delete` command. This is like dismantling a section of the castle according to the blueprints:

```bash
oc delete -k overlay/production
```

## Conclusion

Congratulations, master builder of the Openshift kingdom! By mastering Kustomize, you gain the power to manage and adapt your Kubernetes configurations with ease and precision. Just as a ruler carefully plans and modifies their castle, you can now ensure your applications are tailored to their environments while preserving the integrity of your original configurations. Embrace the power of Kustomize and fortify your Openshift domain with confidence.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>
