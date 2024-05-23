# Templates

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/templates.jpg?raw=true" alt="openshift_templates" width="300" height="300">
</div>

## Objective

Learn how to use Openshift templates to define sets of Kubernetes resource configurations with customizable parameters.

## Prerequisites

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic knowledge of Kubernetes, YAML syntax, and Openshift CLI commands.

## Introduction

Welcome, noble overseer of the Openshift kingdom! In your realm, templates are the blueprints that enable you to create and customize Kubernetes resources with ease. Red Hat's Openshift extends Kubernetes with template resources, allowing you to define, evaluate, and deploy configurations tailored to your needs. Join us as we explore the power of Openshift templates and enhance your control over the Openshift kingdom.

## Understanding Openshift Templates

### The Blueprint of Resources

In the Openshift kingdom, templates are like blueprints stored in the royal library. These blueprints define sets of Kubernetes resource configurations with customizable parameters, allowing you to create various resources such as Pods, Services, and Deployments. With templates, you can standardize and streamline the deployment process, ensuring that your kingdom's resources are consistent and well-organized.

Red Hat provides template resources as a Kubernetes extension, and the Cluster Samples Operator populates these templates in the `openshift` namespace. As the ruler of your realm, you have the power to opt-out of template addition during installation and customize templates to fit the unique needs of your projects.

### Viewing Templates

To view the available templates in the `openshift` namespace, use the following command:

```bash
oc get templates -n openshift
```

This command is like opening a grand tome listing all the blueprints stored in your royal library.

To evaluate a specific template and see its details, use:

```bash
oc describe template <template-name> -n openshift
```

This reveals the intricate designs and parameters of the selected blueprint, providing you with a deeper understanding of its structure.

### Viewing Template Parameters

To see only the parameters that a template uses, the `oc process` command provides the `--parameters` option:

```bash
oc process --parameters <template-name> -n openshift
```

This is akin to examining the key components and customizable elements of your blueprint, allowing you to tailor it to your needs.

You can also view the parameters of a template defined in a file using the `-f` option:

```bash
oc process --parameters -f my-cache-service.yaml
```

### Retrieving Template Manifests

To retrieve the manifest of a template, use the following command:

```bash
oc get template cache-service -o yaml -n openshift
```

This command unfurls the complete blueprint, showing all the detailed configurations and settings defined within.

## Deploying Templates

### Creating Resources from Templates

When it's time to deploy the template, you can use the `--template` parameter with the `new-app` command to create resources directly from the openshift project:

```bash
oc new-app --template=cache-service -p APPLICATION_USER=my-user
```

This command is particularly convenient for non-production environments, allowing you to swiftly create new resources based on your blueprints. However, note that the `new-app` command is useful only for creating new resources, not for updating existing ones.

### Applying Parameters to Templates

To apply parameters to a template and process it, use the `oc process` command. This command can process both local and cluster templates:

```bash
oc process -f my-cache-service.yaml -p APPLICATION_USER=my-user | oc apply -f -
```

This process is like activating a magical spell, transforming the blueprint into tangible resources within your kingdom.

## Conclusion

Congratulations, esteemed steward of the Openshift kingdom! By mastering Openshift templates, you can define, evaluate, and deploy sets of Kubernetes resource configurations with ease. These blueprints ensure that your deployments are consistent, efficient, and tailored to the unique needs of your projects. Embrace the power of templates and fortify your Openshift realm with confidence.

With this knowledge, you hold the key to a well-structured and efficient kingdom, where resources are created and managed with precision and ease. Your kingdom thrives under your vigilant guidance, as you skillfully wield the power of Openshift templates to shape your domain.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>
