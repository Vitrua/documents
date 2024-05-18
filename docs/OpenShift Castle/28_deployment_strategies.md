# Deployment Strategies

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/deploymentstrategies.jpg?raw=true" alt="deployment_strategies" width="300" height="300">
</div>

## Objective

Learn how to select and implement deployment strategies in Openshift to minimize risks and ensure smooth application updates.

## Prerequisites

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic knowledge of Openshift concepts and command-line interfaces (CLI).

## Introduction

Welcome, strategic architect of the Openshift kingdom! Deploying application changes can be fraught with risks such as downtime, bugs, or performance issues. By carefully selecting and implementing deployment strategies, you can minimize these risks and ensure seamless updates. Join us as we explore the various deployment strategies available in Openshift, and learn how to apply them to safeguard your applications within the fortified castle.

## Understanding Deployment Strategies

### The Art of Strategic Deployment

In the magical realm of Openshift, deployment strategies are your tools for updating applications while minimizing impact. Whether you're gradually rolling out updates or replacing all instances at once, choosing the right strategy is crucial for maintaining the kingdom’s stability.

Just as a wise ruler plans the defense of a castle, you must plan your deployments to ensure the safety and efficiency of your applications.

- **RollingUpdate Strategy**: Updates the application in stages, replacing one instance at a time until all are updated. This is the default strategy and ensures minimal downtime. Imagine a skilled knight replacing guards one by one at their posts, ensuring the castle remains protected at all times.
  
- **Recreate Strategy**: Terminates all instances of the application before deploying the new version, causing downtime but ensuring a clean slate. Picture the castle gates closing, all guards being replaced at once, and then reopening with fresh new protectors ready to defend.

## Configuring Deployment Strategies

### Crafting the Deployment Plan

To apply a deployment strategy, you modify the `.spec.strategy.type` property of the Deployment object. Let’s delve into how you can configure these strategies using YAML.

#### Example Usage with YAML

Here’s how to define a RollingUpdate strategy in your deployment configuration:

```yaml title="deployment-strategy-example.yaml"
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp2
spec:
  progressDeadlineSeconds: 600
  replicas: 10
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: myapp2
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 50%
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: myapp2
    spec:
      containers:
      - name: myapp2
        image: myapp:latest
```

Apply this configuration using the command:

```bash
oc apply -f deployment-strategy-example.yaml
```

#### Managing Deployments via CLI

In times of change, even the most strategic plans may require adjustments. To pause and resume a rollout, preventing automatic updates and allowing for controlled deployment, you can command your army like this:

```bash
oc rollout pause deployment/myapp
oc rollout resume deployment/myapp
```

This is akin to pausing the changing of the guard, giving you control over when and how the new guards take their posts.

### Replica Sets

When you create or update a Deployment object, Openshift generates a new ReplicaSet object with the updated pod template. Avoid directly editing ReplicaSet objects; instead, monitor their status as a vigilant ruler would:

```bash
oc get replicaset
```

### Rolling Back Deployments

If an update causes issues, you can roll back to a previous version, much like reverting to a tried and trusted defense strategy:

```bash
oc rollout undo deployment/myapp2
```

Monitor the rollout status with:

```bash
oc rollout status deployment/myapp2
```

### Handling Stuck Rollouts

For DeploymentConfig objects, you can cancel a stuck rollout. Think of this as aborting a flawed plan before it can jeopardize the castle’s defenses:

```bash
oc rollout cancel
```

### Viewing Deployment History

Every wise ruler keeps records of past strategies. List all available revisions:

```bash
oc rollout history deployment/myapp2
```

For details about a specific revision, add the `--revision` option:

```bash
oc rollout history deployment/myapp2 --revision=1
```

## Conclusion

Embark on the journey of mastering deployment strategies within the fortified bastion of Openshift. By understanding and implementing the appropriate strategies, you ensure your applications are updated smoothly, maintaining their performance and resilience within the mystical confines of Openshift.

Just as a wise ruler safeguards their castle with strategic planning and vigilant management, you too can protect your applications and ensure their success within the Openshift kingdom.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>