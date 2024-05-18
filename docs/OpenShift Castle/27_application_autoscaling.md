# Application Autoscaling

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/appautoscaling.jpg?raw=true" alt="application_autoscaling" width="300" height="300">
</div>

## Objective

Understand the mechanisms of horizontal pod autoscaling within the Openshift cluster to ensure your applications can dynamically scale based on demand.

## Prerequisites

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic knowledge of Openshift concepts and command-line interfaces (CLI).
- Resource requests specified for your pods to allow autoscaling based on metrics.

## Introduction

Greetings, noble overseer of the dynamic kingdom! In the fortified bastion of Openshift, the horizontal pod autoscaler acts as the magical force that adjusts your application’s resources in response to the ever-changing demands of the realm. By setting up autoscaling, you ensure that your applications can handle fluctuating workloads, maintaining their performance and resilience. Join us as we delve into the arcane art of application autoscaling, enabling your applications to thrive within the Openshift kingdom.

## Understanding Application Autoscaling

### The Magic of Dynamic Resource Allocation

In the enchanted world of Openshift, the horizontal pod autoscaler (HPA) is your ally in maintaining balance. It uses performance metrics collected by the Openshift Metrics subsystem to automatically adjust the number of pods in a deployment based on demand.

The autoscaler works in a loop, performing these steps every 15 seconds by default:

1. **Retrieve Metrics**: The autoscaler fetches the scaling metric details from the HPA resource.
2. **Collect Metrics**: For each targeted pod, the autoscaler gathers metrics from the metrics subsystem.
3. **Compute Usage Percentage**: It calculates the usage percentage for each pod using the collected metrics and the pod's resource requests.
4. **Calculate Average Usage**: It computes the average usage and resource requests across all targeted pods, establishing a usage ratio.
5. **Make Scaling Decision**: The autoscaler uses this ratio to decide whether to scale the number of pods up or down.

## Configuring Application Autoscaling

### Casting the Autoscaling Spell

To enable autoscaling for your deployment, you can create an HPA resource using the `oc autoscale` command or a YAML manifest.

#### Example Usage with `oc autoscale` Command

Here’s how to create an HPA resource for a deployment named "my-app" to scale between 1 and 10 pods, targeting 75% CPU usage:

```bash
oc autoscale deployment/my-app --min 1 --max 10 --cpu-percent 75
```

This command sets up an autoscaler that adjusts the number of pods based on their CPU usage, scaling up to a maximum of 10 pods when the average CPU usage exceeds 75%.

#### Example Usage with YAML

Alternatively, you can define the HPA resource in a YAML file:

```yaml title="hpa-example.yaml"
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: my-app
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-app
  minReplicas: 1
  maxReplicas: 10
  targetCPUUtilizationPercentage: 80
```

Apply this configuration using the command:

```bash
oc apply -f hpa-example.yaml
```

### Monitoring and Managing Autoscaling

To check if the autoscaler has been correctly created in the current project:

```bash
oc get hpa
```

This command lists the HPAs in the current namespace, showing their status and metrics.

## Conclusion

Embark on the journey of mastering application autoscaling within the fortified bastion of Openshift. By configuring and managing horizontal pod autoscalers, you ensure your applications can dynamically adjust to varying workloads, maintaining their performance and resilience within the mystical confines of Openshift.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>