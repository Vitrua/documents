# Operator Updates

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/opup.jpg?raw=true" alt="opup" width="300" height="300">
</div>

## Objective

Help cluster administrators define and manage operator update policies to ensure the cluster remains functional and up-to-date with bug fixes and new features.

## Introduction

In the grand kingdom of OpenShift, operators are like the skilled artisans who maintain and enhance the castle’s various systems. These artisans, whether they be blacksmiths, masons, or engineers, play a crucial role in ensuring the castle remains fortified and efficient. Keeping these operators updated is essential for the smooth functioning of the cluster. OpenShift provides several tools to help administrators manage operator updates effectively, ensuring that the castle remains secure and operational.

## Prerequisites

- Access to an OpenShift cluster.
- Familiarity with Operator Lifecycle Manager (OLM) and operator management.
- Administrative privileges to manage operator updates and policies.

## Defining Operator Update Policies

### Automatic and Manual Updates

When new techniques or tools are discovered in the kingdom, the master artisans need to decide whether to implement these changes immediately or wait for royal approval. Similarly, when installing an operator, administrators can choose whether updates should be applied automatically by the OLM or require manual approval.

The `installPlanApproval` property in the resource specification dictates this behavior, accepting either `Automatic` or `Manual` values. To manage updates from the web console, navigate to **Operators** > **Installed Operators**.

To retrieve information about subscription resources and install plans, use:
```bash
oc get sub -n openshift-operators web-terminal -o yaml
```

If the operator channel has a newer version, the OLM creates an install plan resource, much like a master plan crafted by the kingdom's engineers. For example:
```bash
oc get installplan -n openshift-operators install-72vnw -o yaml
```

To approve an update manually, edit the install plan to change the `approved` key to `true`:
```bash
oc patch installplan install-72vnw --type merge --patch '{"spec":{"approved":true}}'
```

### Operator Channels and Custom Catalogs

Operator providers can create multiple channels for an operator, much like different guilds that follow distinct practices and update schedules. Administrators can choose which channel to follow based on their update policies, ensuring the castle's operations align with their strategic plans. Additionally, custom catalogs can be created to include specific versions of operators, offering more control over the updates.

## Integrating Operator Updates with Cluster Updates

Before updating the entire kingdom’s infrastructure, it’s essential to review and apply any operator updates required for compatibility. This step ensures that all artisans are ready to support the new changes decreed by the royal council.

If no compatible operator updates are available, uninstalling incompatible operators might be necessary. This is akin to retiring outdated guilds that can no longer serve the kingdom’s needs. Operators can be uninstalled from the web console under **Operators** > **Installed Operators**, or by deleting the subscription and cluster service versions using the `oc` command.

Uninstalling an operator can leave remnants on the cluster, similar to abandoned workshops and tools. Always consult the operator documentation for any cleanup processes to ensure complete removal.

## Example Commands

Here are some practical examples to guide administrators in managing operator updates:

1. **Retrieve Subscription Details**:
    ```bash
    oc get sub -n openshift-operators web-terminal -o yaml
    ```

2. **View Install Plans**:
    ```bash
    oc get installplan -n openshift-operators install-72vnw -o yaml
    ```

3. **Approve an Install Plan**:
    ```bash
    oc patch installplan install-72vnw --type merge --patch '{"spec":{"approved":true}}'
    ```

4. **Uninstall an Operator**:
    ```bash
    oc delete sub -n openshift-operators web-terminal
    oc delete csv -n openshift-operators web-terminal.v1.0.0
    ```

## Conclusion

Managing operator updates is crucial for maintaining a healthy and functional OpenShift cluster. By defining clear update policies and integrating them with overall cluster maintenance, administrators can ensure that their Kubernetes kingdom remains robust and up-to-date. Staying proactive with operator updates will keep the castle running smoothly and efficiently, ready to tackle any challenges that arise. Just as a well-maintained castle withstands the test of time, a well-managed OpenShift cluster can handle the ever-evolving landscape of technology and innovation.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>