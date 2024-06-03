# Project Creation

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/creaproj.jpg?raw=true" alt="creaproj" width="300" height="300">
</div>

## Objective

Understand how to create and manage projects in OpenShift to improve security and user experience, utilizing project templates to customize namespace creation.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Understanding of Kubernetes namespaces and their role in resource isolation.
- Familiarity with OpenShift CLI (`oc` commands) for managing resources.

## Introduction

In the kingdom of OpenShift, creating and managing projects (or namespaces) is akin to establishing new territories within the realm. Each territory must be governed by specific rules and regulations to ensure smooth and secure operations. OpenShift introduces projects to enhance security and improve users' experience when working with namespaces. This approach ensures that territories are well-defined and managed efficiently.

## Projects and Project Requests

### Differentiating Resource Listing and Viewing

Listing resources and viewing individual resources are distinct operations. Just as a king might grant different levels of access to his courtiers, administrators can grant users permissions to view specific namespaces. However, listing all namespaces requires a separate permission, ensuring that users only see what they are authorized to see.

### Introducing Projects

OpenShift introduces the *Project* resource type to improve security and user experience. When users query to list projects, the OpenShift API server lists namespaces, filters the ones visible to the user, and returns them in project format. This filtering mechanism ensures that users only see the projects they have access to, much like how citizens in the kingdom only have access to their own territories.

### ProjectRequest Resource Type

Additionally, OpenShift introduces the *ProjectRequest* resource type. When users create a project request, the OpenShift API server creates a namespace from a template. This feature allows cluster administrators to customize namespace creation, enabling a self-service management model for namespaces. Users can create namespaces without the ability to modify namespace metadata, ensuring a controlled and secure environment.

## Planning a Project Template

When planning a project template, you can add any namespaced resource to it. These resources help define the rules and limits for the new territories within the kingdom.

### Typical Resources to Include

1. **Roles and Role Bindings**:
   - Grant specific permissions in new projects.
   - The default template grants the *admin* role to the user who requests the project.
   - Additional granular permissions can be added over specific resource types, ensuring that users have the appropriate level of access, much like assigning different roles to members of the royal court.

2. **Resource Quotas and Limit Ranges**:
   - Suggested to add quotas to the project template to ensure that all new projects have resource limits.
   - Adding cluster resource quotas is also beneficial, similar to setting boundaries for the territories to prevent resource overuse and ensure fair distribution.

3. **Network Policies**:
   - Add network policies to the template to enforce organizational network isolation requirements.
   - These policies ensure secure and isolated communication channels, akin to setting up guarded paths and gates within the kingdom.

### Example of a Project Template

Here is an example of a project template configuration:

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

In this example, the project template includes configurations for a namespace, resource quotas, limit ranges, and network policies. These elements are essential for maintaining order and ensuring that each new territory adheres to the kingdom's regulations.

## Conclusion

Creating and managing projects in OpenShift is a crucial task that ensures secure and efficient operations within the cluster. By utilizing project templates, administrators can enforce consistent rules and limits across all new namespaces. This approach not only improves security but also enhances user experience, providing a well-organized and controlled environment akin to a well-governed kingdom.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>