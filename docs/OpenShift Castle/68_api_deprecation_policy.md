# Kubernetes API Deprecation Policy

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/apidep.jpg?raw=true" alt="apidep" width="300" height="300">
</div>

## Objective

Help administrators navigate the deprecation and removal of Kubernetes API versions, ensuring that their clusters remain up-to-date and functional.

## Introduction

In the grand kingdom of Kubernetes, the API serves as the central hall where all commands are issued and executed. Just as a well-managed kingdom evolves its laws and practices to remain effective, Kubernetes updates its APIs to ensure robustness and security. Understanding the deprecation policy of Kubernetes APIs is essential for maintaining the harmony and functionality of your clusters.

## Prerequisites

- Access to an OpenShift cluster.
- Familiarity with Kubernetes API and resource management.
- Administrative privileges to view and manage API resources.

## Understanding API Versions

In our Kubernetes kingdom, API versions are like the evolving laws:
- **Experimental**: Newly introduced laws being tested.
- **Pre-release**: Laws that are being fine-tuned based on feedback.
- **Stable**: Well-established laws that are widely adopted.

To check the current version of a specific resource, such as cronjobs, use:
```bash
oc api-resources | egrep '^NAME|cronjobs'
```

## Deprecation and Removal Policy

When a new stable version of a feature is decreed, any older beta versions are marked as deprecated, similar to old laws being phased out. These deprecated versions are typically removed after three Kubernetes releases. It's crucial to track these changes to prevent any disruptions in your operations.

### Handling Deprecation Warnings

If you issue a command using a deprecated API version, the API server responds with a deprecation warning, much like the castle's heralds announcing that certain laws will soon change. This warning includes the current version of the cluster.

### Handling Removed API Versions

Attempting to use an API version that has been removed is like trying to follow an old law that is no longer valid. The API server will return an error, indicating that the version is not supported in the cluster.

## Monitoring API Requests

To ensure your kingdom’s operations are up-to-date, monitor the API request counts to identify usage of deprecated API versions. The *REMOVEDINRELEASE* column indicates when a specific API version will be removed:
```bash
oc get apirequestcounts | awk '{if(NF==4){print $0}}'
```

To gather detailed information about the actions for a resource and identify who performed them, use a JSONPath filter:
```bash
FILTER='{range .status.currentHour..byUser[*]}{..byVerb[*].verb}{","}{.username}{","}{.userAgent}{"\n"}{end}'
TYPE=apirequestcount.apiserver.openshift.io/cronjobs.v1beta1.batch
echo ${TYPE} ; oc get ${TYPE} -o jsonpath="${FILTER}" | column -t -s ',' -N "Verbs,Username,UserAgent"
```

This command helps track which knights and courtiers (users and systems) are still relying on old laws (deprecated API versions).

## Conclusion

Keeping your Kubernetes API usage current is akin to ensuring that your kingdom's laws are up-to-date. Regularly reviewing deprecation warnings and planning upgrades accordingly will maintain a robust and efficient OpenShift environment. By staying informed and proactive, you can ensure that your Kubernetes kingdom remains secure and well-governed.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>