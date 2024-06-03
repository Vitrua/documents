# Updating the Cluster

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/upclu.jpg?raw=true" alt="upclu" width="300" height="300">
</div>

## Objective

Learn how to update your OpenShift cluster using both the web console and the command-line interface (CLI), while ensuring all prerequisites are met.

## Prerequisites

Before updating your OpenShift cluster, ensure the following:
1. All operators installed through the Operator Lifecycle Manager (OLM) are updated to their latest versions.
2. For production clusters, ensure the update channel is set to *stable*.

## Introduction

In the kingdom of OpenShift, maintaining an up-to-date infrastructure is akin to ensuring the castle is fortified with the latest defenses and technologies. Regular updates bring new features, security enhancements, and bug fixes, much like reinforcements and upgrades to a castle’s defenses. As a wise ruler, it’s essential to follow a structured process to update the cluster, ensuring the realm remains secure and efficient.

## Updating the Cluster via Web Console

The web console provides an intuitive interface for initiating cluster updates.

1. Navigate to **Administration** > **Cluster Settings**.
2. When a new update is available, click **Update now** to begin the process.

**Note:** Rolling back your cluster to an earlier version is not supported. If your update fails to complete, contact Red Hat support.

## Updating the Cluster via Command-Line Interface (CLI)

For those who prefer the precision of command-line tools, the CLI offers a powerful way to manage cluster updates.

### Step-by-Step CLI Update Process

1. **Update All Operators:**
   Ensure all operators installed through the OLM are updated to the latest version before updating the OpenShift cluster. This is akin to preparing all the castle’s defenses before a major upgrade.

2. **Retrieve Cluster Version and Update Channel Information:**
   - Retrieve the current cluster version:
     ```bash
     oc get clusterversion
     ```
   - Review the current update channel information. Ensure it reads *stable* if running in production:
     ```bash
     oc get clusterversion -o jsonpath='{.items[0].spec.channel}{"\n"}'
     ```

3. **View Available Updates:**
   Discover the available updates and note the version number to apply. This step is like surveying the available reinforcements and choosing the best fit for your castle.
   ```bash
   oc adm upgrade
   ```

4. **Apply the Update:**
   - To install the latest available update:
     ```bash
     oc adm upgrade --to-latest=true
     ```
   - To install a specific version, where `VERSION` corresponds to an available version:
     ```bash
     oc adm upgrade --to=VERSION
     ```

5. **Review the Update Status:**
   Once the update process is initiated, monitor the status of the Cluster Version Operator (CVO) and the installed cluster operators. This ensures all components are updating correctly, similar to overseeing the progress of castle upgrades.
   ```bash
   oc get clusterversion
   oc get clusteroperators
   ```

6. **Monitor the Update Process:**
   Review the cluster version history and monitor the status of the update. It might take some time for all objects to finish updating. Successful updates have a *Completed* state, while incomplete updates have a *Partial* state.
   ```bash
   oc describe clusterversion
   ```

   If the update fails to complete, the CVO reports the status of any blocking components and attempts to reconcile the update. Contact Red Hat support if the issue persists.

7. **Confirm the Update:**
   After the process completes, confirm that the cluster is updated to the new version. This final check ensures the castle’s defenses are now fully upgraded and ready to protect the realm.
   ```bash
   oc get clusterversion
   ```

## Conclusion

Updating your OpenShift cluster is a crucial task that ensures your environment remains secure, efficient, and up-to-date with the latest features. By following these steps, whether through the web console or CLI, you can manage the updates seamlessly, much like a wise ruler upgrading the castle’s defenses to protect the kingdom. Remember, while rolling back is not supported, Red Hat support is always available to assist with any issues during the update process.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>