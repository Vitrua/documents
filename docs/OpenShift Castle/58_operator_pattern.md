# The Operator Pattern

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/oppat.jpg?raw=true" alt="oppat" width="300" height="300">
</div>

## Objective

Understand the Operator pattern in Kubernetes and OpenShift, and learn how to deploy and manage operators to handle complex workloads effectively.

## Introduction

In the grand kingdom of OpenShift, managing complex workloads requires more than just basic resources—it demands the expertise of specialized agents known as Operators. These Operators, much like skilled artisans in the castle, understand the intricate details of their specific tasks, ensuring that everything runs smoothly and efficiently within the digital realm.

## The Operator Pattern

The Operator pattern is a design used to create reusable software that manages complex workloads. Operators define Custom Resources (CRs), which contain the necessary information to deploy and manage these workloads. Think of Operators as master architects in the castle who not only design the structures but also ensure their ongoing maintenance and upgrades, keeping the kingdom in perfect working order.

## Deploying Operators

Various pieces of software implement the Operator pattern in different ways, providing flexible and powerful tools to manage your workloads, akin to having different guilds of craftsmen working together to maintain and enhance the castle.

### Cluster Operators

Cluster operators provide essential platform services in OpenShift, such as the web console and the OAuth server. The Cluster Version Operator (CVO) acts as the kingdom's chief engineer, handling the installation and updating of cluster operators during the OpenShift installation and update processes.

To check the status of cluster operators, you can use the following command, much like a royal decree to gather status reports from various parts of the kingdom:

```bash
oc get clusteroperator
```

Alternatively, from the web console, navigate to **Administration** > **Cluster Settings**, and then click the **ClusterOperators** tab. This view provides a comprehensive overview of the current state of all cluster operators, similar to a council meeting where all updates are reviewed.

### Add-on Operators

OpenShift includes the Operator Lifecycle Manager (OLM) to assist users in installing and updating operators within a cluster. These operators, managed by the OLM, are referred to as add-on operators, distinguishing them from cluster operators that provide core platform services. Think of these add-on operators as specialized guilds that bring new capabilities to the castle.

The OLM uses operator catalogs—container images that contain information about available operators, including descriptions and versions. For each available operator, the OLM creates a resource of the PackageManifest type. The web console also displays available operators and provides a wizard to simplify the installation process. Alternatively, operators can be installed using the Subscription Custom Resource (CR) and other related CRs.

Operators installed via the OLM have a distinct lifecycle, allowing administrators to manage installations, updates, and removals independently from cluster updates. This independence is like having guilds that can operate autonomously, ensuring that the kingdom continues to function smoothly even as new improvements are made.

### Other Operators

Software providers can create software that follows the Operator pattern and distribute it as manifests, Helm charts, or other mechanisms. This flexibility allows for a wide range of applications and tools to be integrated into the OpenShift ecosystem, each managed by its specialized operator. Imagine this as various craftsmen and experts from distant lands bringing their unique skills to enhance the castle's operations.

## Conclusion

The Operator pattern in OpenShift is a powerful method for managing complex workloads by leveraging the expertise of specialized agents known as Operators. Whether deploying core platform services with cluster operators or adding new capabilities with add-on operators, the Operator Lifecycle Manager (OLM) provides a robust framework for managing these essential components. By understanding and utilizing the Operator pattern, administrators can ensure their clusters are as well-maintained and efficient as the most meticulously run kingdom, with each guild and artisan contributing to the prosperity and stability of the digital realm.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>