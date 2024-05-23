# Authenticating API Requests

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/authentication.jpg?raw=true" alt="authentication" width="300" height="300">
</div>

## Objective

Learn how to authenticate API requests in OpenShift using OAuth access tokens and X.509 client certificates, and understand how to authenticate as a cluster administrator.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Basic knowledge of OpenShift concepts and command-line interfaces (CLI).

## Introduction

Greetings, vigilant guardian of the OpenShift kingdom! Ensuring secure access to your kingdom's API is paramount for maintaining order and protecting valuable resources. OpenShift offers two primary methods for authenticating API requests: OAuth access tokens and X.509 client certificates. By mastering these authentication methods, you can safeguard your realm and manage access effectively.

## Authenticating API Requests

In the enchanted lands of OpenShift, the magical process of authenticating API requests ensures that only trusted entities can interact with the kingdom's precious resources.

### OAuth Access Tokens

The **OAuth access token** is like a magical key granted by the Authentication operator, which runs an OAuth server. This key allows users to access the API and perform actions based on their roles and permissions.

- **Usage**: OAuth access tokens are generated after a successful login via an identity provider, much like a knight receiving a seal of approval to enter the royal court. These tokens are used to authenticate API requests, ensuring that only those with proper authorization can perform specific actions.

### X.509 Client Certificates

**X.509 client certificates** serve as trusted insignias, proving the identity of a client to the API server. These certificates are included in the kubeconfig file created during the OpenShift installation.

- **Usage**: X.509 certificates authenticate API requests by verifying the client's identity using a secure certificate, akin to presenting a royal decree that confirms one's noble status and right to access the kingdom's resources.

## Authenticating as Cluster Administrator

Before you can manage users and configure identity providers, you must authenticate as an administrator. Let's explore the methods to achieve this, ensuring you have the keys to the kingdom.

### Authenticating with the X.509 Certificate

During installation, the OpenShift installer creates a unique kubeconfig file in the auth directory. This file contains specific details and parameters for the CLI to connect a client to the correct API server, including an X.509 certificate. Installation logs provide the location of the kubeconfig file:

```log
INFO Run 'export KUBECONFIG=root/auth/kubeconfig' to manage the cluster with 'oc'.
```

To use the kubeconfig file to authenticate `oc` commands, follow these steps:

1. **Copy the kubeconfig file**: Transfer the file to your workstation, much like carrying a royal decree to your chambers.
2. **Set the KUBECONFIG environment variable**: Define the path to the kubeconfig file.

```bash
export KUBECONFIG=/home/user/auth/kubeconfig
oc get nodes
```

Alternatively, specify the kubeconfig file directly with the `oc` command:

```bash
oc --kubeconfig /home/user/auth/kubeconfig get nodes
```

### Authenticating with the kubeadmin Virtual User

After installation, OpenShift creates the **kubeadmin virtual user**. The kubeadmin secret in the kube-system namespace contains the hashed password for this user. The installation logs provide the kubeadmin credentials:

```log
INFO The cluster is ready when 'oc login -u kubeadmin -p shdU_trbi_6ucX_edbu_aqop'
```

As the esteemed ruler, you can use these credentials to access the cluster and perform administrative tasks.

### Deleting the Virtual User

To enhance cluster security, delete the kubeadmin user credentials after defining an identity provider, creating a user, and assigning that user the cluster-admin role:

```bash
oc delete secret kubeadmin -n kube-system
```

Even after deleting the virtual user, you can still log in through the kubeconfig file, ensuring that your kingdom's gates remain secure yet accessible to trusted administrators.

## Conclusion

Wise steward of the OpenShift kingdom, you now hold the knowledge to authenticate API requests securely and manage your domain effectively. By leveraging OAuth access tokens and X.509 client certificates, you can ensure that only trusted entities access your API. As a cluster administrator, you possess the authority to manage users and configure identity providers, further fortifying your realm's security. Embrace these authentication methods to safeguard your kingdom and maintain order within its boundaries.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>
