# Using Operators

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/usingop.jpg?raw=true" alt="usingop" width="300" height="300">
</div>

## Objective

Learn how to use and troubleshoot operators in Kubernetes by examining custom resource definitions and understanding operator workloads.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Basic knowledge of Kubernetes, including custom resource definitions (CRDs).
- Familiarity with YAML syntax for configuration files.

## Introduction

In the bustling kingdom of OpenShift, operators are the master craftsmen who bring complex tasks to life. They handle intricate workloads and ensure everything runs smoothly within the kingdom. To effectively use these operators, administrators need to understand how to create and manage custom resources, as well as how to troubleshoot any issues that arise.

## Using Operators

To make the most of an operator, it's essential to review its documentation. This documentation often guides administrators on how to use the operator by creating instances of its custom resources, much like following a detailed manual to build a complex structure.

### Learning About Custom Resource Definitions

To learn about the available custom resource definitions (CRDs) provided by an operator, you can examine the operator's details. This is akin to reviewing the blueprints and specifications of the tasks the craftsmen can perform.

For example, you can examine the custom resource definitions owned by the `metallb-operator` using the following command:

```bash
oc get csv metallb-operator.4.14.0-202405201438 -o jsonpath="{.spec.customresourcedefinitions.owned[*].name}"
```

This command retrieves the names of the custom resource definitions owned by the specified operator. Additionally, you can use `oc explain` to view detailed descriptions of individual custom resource definitions, much like consulting a detailed guidebook for each tool and resource available in the kingdom.

## Troubleshooting Operators

Operators typically manage two kinds of workloads within the kingdom:

1. **Operator Workload**: This workload monitors custom resources and ensures they are properly managed and maintained. It's like the master craftsman overseeing various projects.
2. **Instance Workloads**: These are the workloads created by individual instances of the custom resources. They represent the actual tasks being carried out based on the operator's instructions.

To troubleshoot these workloads, it's important to understand the deployments created by the Operator Lifecycle Manager (OLM) during the installation of an operator. These deployments often correspond to the operator workload, detailing how the master craftsman sets up their operations.

### Examining Operator Workloads

The `spec.install.spec.deployments` field in the ClusterServiceVersion (CSV) contains the deployments that the OLM creates when installing an operator. This is where you can find the details of the operator workload, much like examining the organizational chart of the craftsmen and their assigned tasks.

To view this information, you can use a command like:

```bash
oc get csv metallb-operator.4.14.0-202405201438 -o jsonpath="{.spec.install.spec.deployments[*].name}"
```

This command retrieves the names of the deployments specified in the CSV, providing insights into the operator's setup.

## Conclusion

In the kingdom of OpenShift, understanding how to use and troubleshoot operators is crucial for maintaining a well-managed and efficient environment. By reviewing operator documentation, examining custom resource definitions, and understanding the workloads managed by operators, administrators can ensure that their digital realm operates smoothly. This knowledge equips administrators with the tools needed to manage complex tasks and resolve issues, ensuring that the kingdom of OpenShift remains prosperous and secure.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>
