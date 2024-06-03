# Deprecated and Removed Features in OpenShift

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/featope.jpg?raw=true" alt="featope" width="300" height="300">
</div>

## Objective

Assist administrators in managing deprecated and removed features in OpenShift to ensure smooth cluster updates and continued functionality.

## Introduction

In the grand kingdom of OpenShift, deprecated features are like old customs that need to be retired for the kingdom to flourish. Recognizing and managing these deprecated APIs is essential to maintaining the realm’s health and security. OpenShift provides mechanisms to alert administrators when deprecated APIs are in use and requires explicit acknowledgment before cluster updates to ensure a smooth transition to newer versions.

## Prerequisites

- Access to an OpenShift cluster.
- Familiarity with OpenShift monitoring and Prometheus.
- Administrative privileges to manage cluster updates and configurations.

## Deprecated and Removed Features

OpenShift includes two specific alerts for deprecated API usage:
- **APIRemovedInNextReleaseInUse**: Triggered for APIs scheduled for removal in the next OpenShift Container Platform release.
- **APIRemovedInNextEUSReleaseInUse**: Triggered for APIs scheduled for removal in the next Extended Update Support (EUS) release.

### Extracting Deprecated API Alerts

To keep the kingdom of OpenShift secure, administrators must identify and manage deprecated APIs. By extracting alerts in JSON format from the Prometheus stateful set and filtering the results, you can identify which deprecated APIs are still in use. This process is akin to the royal scribes keeping track of old laws that need to be updated.

Run the following commands to retrieve deprecated API alerts:
```bash
oc exec -it statefulset/prometheus-k8s -c prometheus \
-n openshift-monitoring -- \
curl -fsSL 'http://localhost:9090/api/v1/alerts' | jq . > alerts.json

jq '[.data.alerts[] |
select(.labels.alertname=="APIRemovedInNextReleaseInUse" or
.labels.alertname=="APIRemovedInNextEUSReleaseInUse")]' < alerts.json
```

### Explicit Acknowledgment Before Cluster Updates

Before the kingdom can adopt new laws (cluster updates), administrators must acknowledge deprecated APIs. This acknowledgment is necessary to ensure that all components using outdated APIs are migrated to the new versions, preventing disruptions during the transition.

To provide a manual acknowledgment, use the following command:
```bash
oc patch configmap admin-acks -n openshift-config --type=merge --patch '{"data":{"ack-4.11-kube-1.25-api-removals-in-4.12":"true"}}'
```

This process ensures that the council (administrators) is aware of the changes and has taken the necessary steps to update the kingdom’s practices (API usage).

## Conclusion

Managing deprecated and removed features in OpenShift is like ensuring that the kingdom’s laws and customs remain relevant and effective. By monitoring alerts for deprecated APIs and providing explicit acknowledgments before updates, administrators can maintain a secure and efficient OpenShift environment. Staying informed and proactive in handling these changes will ensure the continued prosperity of the Kubernetes kingdom.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>