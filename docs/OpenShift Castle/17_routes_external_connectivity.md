# Routes for External Connectivity

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/concealed.jpg?raw=true" alt="routes" width="300" height="300">
</div>

## Objective

Learn how to expose applications to external networks in the mystical realms of Openshift through routes.

## Prerequisites

To embark on this journey of routes for external connectivity, you'll need:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic understanding of Openshift concepts and command-line interfaces (CLI).

## Introduction

Welcome, adventurer, to the realm of routes for external connectivity within the enchanted confines of Openshift. Here, amidst the shifting currents of digital networks, lies the key to exposing applications to the outside world. Join us as we unravel the mysteries of routes and learn how to pave pathways for external access to your applications.

## Routes for External Connectivity

### Exposing Applications to the Outside World

In Openshift, routes provide a means to expose applications to external networks, allowing them to be accessed with unique hostnames that are publicly accessible. Routes rely on Kubernetes ingress controllers to redirect traffic from public IP addresses to pods, offering additional features such as TLS re-encryption, TLS passthrough, and support for blue-green deployments.

#### Creating Routes with `oc expose`

To create a route in Openshift, troubleshooters can utilize the `oc expose` command, specifying parameters such as hostname and service:

```bash
oc expose service <service-name> --hostname <hostname>
```
e.g.:
```bash
oc expose service nginx --hostname castle-of-dreams.example.com
```

If the hostname is omitted, Openshift generates a hostname with the following structure: `<route-name>-<project-name>.<default-domain>`

#### Minimal Route Definition

A minimal definition for a route typically includes the following:

```yaml
kind: Route
apiVersion: route.openshift.io/v1
metadata:
  name: <route-name>
spec:
  host: <hostname>
  to:
    kind: Service
    name: <service-name>
  port:
    targetPort: <target-port>
```
e.g.:
```yaml
kind: Route
apiVersion: route.openshift.io/v1
metadata:
  name: castle-of-dreams-route
spec:
  host: castle-of-dreams.example.com
  to:
    kind: Service
    name: nginx
  port:
    targetPort: 80
```

#### Deleting Routes

To delete a route in Openshift, troubleshooters can use the following command:

```bash
oc delete route <route-name>
```
e.g.:
```bash
oc delete route castle-of-dreams-route
```

Embark on this journey of routes for external connectivity, as we pave pathways for accessing applications from the outside world within the mystical confines of the Openshift castle.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>
