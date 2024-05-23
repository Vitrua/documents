# Managing Users with the HTPasswd Identity Provider

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/htpasswd.jpg?raw=true" alt="htpasswd" width="300" height="300">
</div>

## Objective

Learn how to manage user credentials using the HTPasswd Identity Provider in OpenShift by creating, updating, and deleting users, as well as updating the HTPasswd secret.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Basic knowledge of OpenShift concepts and command-line interfaces (CLI).

## Introduction

Welcome, guardian of the OpenShift kingdom! As the keeper of the realm, managing user credentials and ensuring secure access to your cluster is crucial. By using the HTPasswd Identity Provider, you can efficiently manage user credentials, ensuring only trusted individuals gain access to your kingdom's treasures.

## Managing Users with the HTPasswd Identity Provider

### Step 1: Creating an HTPasswd File

In the bustling courtyard of your castle, creating an HTPasswd file is akin to crafting a list of trusted knights who can access the kingdom. Use the following command to create this file:

```bash
htpasswd -c -B -b /tmp/htpasswd student redhat123
```

To add or update credentials for a user, use:

```bash
htpasswd -b /tmp/htpasswd student redhat1234
```

And to delete credentials for a user, use:

```bash
htpasswd -D /tmp/htpasswd student
```

### Step 2: Creating the HTPasswd Secret

With the list of trusted knights prepared, the next step is to store it securely in the royal vaults, known in OpenShift as secrets. Create the HTPasswd secret with:

```bash
oc create secret generic htpasswd-secret --from-file htpasswd=/tmp/htpasswd -n openshift-config
```

### Step 3: Extracting Secret Data

When the time comes to update the list of knights, ensure you are working with the most current version. Extract the secret data:

```bash
oc extract secret/htpasswd-secret -n openshift-config --to /tmp/ --confirm
```

### Step 4: Updating the HTPasswd Secret

After updating the list, store the new version back in the royal vaults:

```bash
oc set data secret/htpasswd-secret --from-file htpasswd=/tmp/htpasswd -n openshift-config
```

Monitor the redeployment of authentication pods to ensure the changes take effect:

```bash
watch oc get pods -n openshift-authentication
```

## Deleting Users and Identities

In the kingdom, removing a knight from service requires careful steps to ensure their access is fully revoked. Follow these steps to delete users and their identities.

### Step 1: Deleting the User from HTPasswd

Remove the user from the HTPasswd file:

```bash
htpasswd -D /tmp/htpasswd manager
```

### Step 2: Updating the Secret

Update the secret to remove the user's credentials from the royal vaults:

```bash
oc set data secret/htpasswd-secret --from-file htpasswd=/tmp/htpasswd -n openshift-config
```

### Step 3: Removing the User Resource

Remove the user resource from the OpenShift kingdom:

```bash
oc delete user manager
```

### Step 4: Deleting the Identity Resource

Find and delete the identity resource associated with the user:

```bash
oc get identities | grep manager
oc delete identity my_htpasswd_provider:manager
```

## Conclusion

Noble guardian, you now possess the knowledge to manage user credentials using the HTPasswd Identity Provider. By creating, updating, and deleting users and their identities, you can maintain the security of your OpenShift kingdom. With these skills, you ensure that only trusted knights can access your realm, safeguarding its treasures and maintaining order.

Embrace your role as the vigilant protector of the OpenShift kingdom, and may your reign be secure and prosperous!

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>
