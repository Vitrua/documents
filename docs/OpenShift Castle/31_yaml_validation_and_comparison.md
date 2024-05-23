# YAML Validation and Resource Comparison

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/yamlvalidation.jpg?raw=true" alt="yaml_validation" width="300" height="300">
</div>

## Objective

Learn how to validate YAML files and compare resources in Openshift to ensure error-free deployments.

## Prerequisites

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic knowledge of YAML syntax and Openshift command-line interfaces (CLI).

## Introduction

Welcome back, vigilant custodian of the Openshift kingdom! As you manage and deploy resources in your realm, ensuring the accuracy and validity of your configuration files is crucial. Just as a wise ruler meticulously inspects every decree before it is issued, you must validate your YAML files to prevent errors and ensure smooth deployments. Additionally, comparing resources allows you to see changes before applying them, much like reviewing the plans for castle upgrades. Join us on this journey as we master the arts of YAML validation and resource comparison to maintain the stability and security of your Openshift domain.

## YAML Validation

### The Importance of Validation

In the Openshift kingdom, validating your YAML files is akin to checking the accuracy of a royal decree. It ensures that the configurations are correct and free of errors before they are applied, preventing disruptions and maintaining the smooth operation of your applications.

### Server-Side Validation

To validate a YAML file before applying changes to a resource, use the `--dry-run=server` and `--validate=true` flags. The `--dry-run=server` option submits a server-side request without persisting the resource, while the `--validate=true` option uses a schema to validate the input and fails the request if it is invalid. This is like consulting with the royal council to verify the decree before issuing it:

```bash
kubectl apply -f ~/my-app/example-deployment.yaml --dry-run=server --validate=true
```

### Client-Side Validation

For a quick check that prints only the object that would be sent to the server, use the `--dry-run=client` option. This is akin to drafting the decree and reviewing it before presenting it to the council:

```bash
kubectl apply -f ~/my-app/example-deployment.yaml --dry-run=client
```

## Comparing Resources

### The Art of Comparison

Before making changes to your resources, it is wise to review the differences between the current live objects and the manifests. This practice helps you understand the impact of your changes and ensures that they align with your intentions. Think of this as comparing the old and new plans for a castle upgrade to ensure all improvements are beneficial.

### Using `kubectl diff`

The `kubectl diff` command allows you to review the differences between live objects and manifests. This command is like holding up two versions of a map to see what has changed:

```bash
kubectl diff -f example-deployment.yaml
```

By comparing the live state with your desired state, you can catch potential issues before they affect your running applications.

## Conclusion

Congratulations, meticulous steward of the Openshift kingdom! By mastering YAML validation and resource comparison, you ensure that your deployments are accurate and error-free, maintaining the stability and security of your applications. Just as a wise ruler carefully reviews every decree and plan, you too can safeguard your Openshift domain by validating and comparing resources before applying changes.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>