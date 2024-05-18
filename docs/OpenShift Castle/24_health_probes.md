# Application of Health Probes

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/probes.jpg?raw=true" alt="health_probes" width="300" height="300">
</div>

## Objective

Explore the crucial role of health probes in maintaining the well-being of your applications within the Openshift cluster.

## Prerequisites

Before beginning your journey into health probes, ensure you have:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic understanding of Openshift concepts and command-line interfaces (CLI).

## Introduction

Greetings, vigilant guardian of application health! Within the fortified bastion of Openshift, health probes serve as your ever-watchful sentinels, constantly monitoring the vitality of your applications. As the steward of application well-being, you wield the power to deploy readiness, liveness, and startup probes, ensuring that your applications thrive within the mystical realm of Openshift. Join us as we delve into the art of configuring and applying health probes, fortifying your applications against the perils of downtime.

## Understanding Health Probes

### The Watchful Sentinels of Your Application

In the enchanted world of Openshift, health probes are your watchful sentinels, each with a unique role to play:

- **Readiness Probes**: Ensure your application is ready to serve requests.
- **Liveness Probes**: Confirm that your application is running and healthy.
- **Startup Probes**: Verify that your application has successfully started.

These probes can perform tests using HTTP GET requests, container commands, or TCP socket connections. Timing variables, such as how often the probe runs and how many attempts it should make before failing, help fine-tune their behavior.

## Configuring Health Probes

### Crafting the Sentinels

Health probes can be added to your workload resources, such as deployments, by updating and applying a YAML file or by using the `oc edit` command.

#### Example Usage with YAML

In this example, a liveness probe is configured for a container named "my-app":

```yaml title="liveness-probe-deployment.yaml"
apiVersion: apps/v1
kind: Deployment
metadata:
  name: liveness-probe-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: my-app:latest
        livenessProbe:
          failureThreshold: 10
          periodSeconds: 5
          httpGet:
            path: /health
            port: 3000
```

This manifest sets up a liveness probe to check the `/health` endpoint every 5 seconds, failing after 10 unsuccessful attempts. Apply this configuration using the command:

```bash
oc create -f liveness-probe-deployment.yaml
```

#### Configuring Probes via CLI

You can also set up health probes directly through the CLI. For example, to add a readiness probe to a deployment named "my-app":

```bash
oc set probe deployment/my-app \
--readiness \
--failure-threshold 10 \
--period-seconds 5 \
--get-url http://:8080/healthz
```

## Conclusion

Embark on the journey of deploying health probes within the fortified bastion of Openshift. By mastering the art of configuring readiness, liveness, and startup probes, you ensure your applications are resilient and responsive, maintaining their vitality within the mystical confines of Openshift.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>