# Creating and Configuring a Project Template

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/projtemplm.jpg?raw=true" alt="projtemplm" width="300" height="300">
</div>

## Objective

Learn to create and configure project templates in OpenShift to customize namespace creation, ensuring that new projects adhere to organizational standards and resource limits.

## Introduction

In the kingdom of OpenShift, creating project templates is akin to crafting blueprints for new territories. These templates ensure that every new project is established with the necessary resources, roles, and policies, much like how a wise ruler ensures that new settlements are well-planned and governed.

## Creating a Project Template

Project templates in OpenShift use the same template feature as the `oc new-app` command. This flexibility allows administrators to create comprehensive templates that can be reused whenever a new project is requested.

### Generating an Initial Template

To create an initial project template, use the following command:

```bash
oc adm create-bootstrap-project-template -o yaml > file
```

This command generates a basic template and outputs it to a file. This file can then be modified to include the required resources for new namespaces.

### Modifying the Template

It's often beneficial to create the namespace and manually adjust the resources in YAML format until the desired behavior is achieved. Once you have finalized the configuration, replace the namespace name with the project name placeholder.

Here is an example of how you can modify the template:

```yaml
apiVersion: template.openshift.io/v1
kind: Template
metadata:
  name: project-template
objects:
  - apiVersion: v1
    kind: Namespace
    metadata:
      name: ${PROJECT_NAME}
  - apiVersion: v1
    kind: ResourceQuota
    metadata:
      name: ${PROJECT_NAME}-quota
      namespace: ${PROJECT_NAME}
    spec:
      hard:
        requests.cpu: "1"
        requests.memory: 1Gi
        limits.cpu: "2"
        limits.memory: 2Gi
  - apiVersion: v1
    kind: LimitRange
    metadata:
      name: ${PROJECT_NAME}-limit-range
      namespace: ${PROJECT_NAME}
    spec:
      limits:
        - default:
            memory: 512Mi
          defaultRequest:
            memory: 256Mi
          type: Container
  - apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
      name: allow-all
      namespace: ${PROJECT_NAME}
    spec:
      podSelector: {}
      policyTypes:
      - Ingress
      - Egress
parameters:
  - name: PROJECT_NAME
    description: The name of the project
    required: true
```

### Creating the Template Resource

Once the template is ready, create the template resource in the `openshift-config` namespace with the following command:

```bash
oc create -f template -n openshift-config
```

This command registers the new template, making it available for use when creating projects.

## Configuring the Project Template

To configure OpenShift to use the new project template, update the `projects.config.openshift.io/cluster` resource. Modify the `spec` section to reference the new template.

Here is an example of the configuration:

```yaml
apiVersion: config.openshift.io/v1
kind: Project
metadata:
  name: cluster
spec:
  projectRequestTemplate:
    name: project-request
```

### Reverting to the Original Template

If you need to revert to the original project template, clear the `spec` resource to match the `spec: {}` format:

```yaml
apiVersion: config.openshift.io/v1
kind: Project
metadata:
  name: cluster
spec: {}
```

## Conclusion

Creating and configuring project templates in OpenShift is a powerful way to standardize and control the creation of new namespaces. By carefully crafting these templates, administrators can ensure that new projects are established with the necessary resources, roles, and policies. This approach promotes consistency and security, much like a well-governed kingdom ensures that new settlements are well-planned and managed.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>