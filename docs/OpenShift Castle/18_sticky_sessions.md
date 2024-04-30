# Sticky Sessions

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/sticky.jpg?raw=true" alt="sticky_sessions" width="300" height="300">
</div>

## Objective

Learn how to configure sticky sessions in the mystical realms of Openshift to maintain session persistence for user requests.

## Prerequisites

To embark on this journey of sticky sessions, you'll need:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic understanding of Openshift concepts and command-line interfaces (CLI).

## Introduction

Welcome, traveler, to the realm of sticky sessions within the enchanted confines of Openshift. Here, amidst the ebb and flow of digital traffic, lies the art of maintaining session persistence for user requests. Join us as we delve into the mysteries of sticky sessions and learn how to configure them to ensure seamless user experiences.

## Sticky Sessions

### Configuring Session Persistence

RHOCP utilizes cookies to configure session persistence for ingress and route resources. The ingress controller selects an endpoint to handle user requests and creates a cookie for the session. This cookie is then passed back in response to the request, allowing the ingress controller to route subsequent requests to the same pod, ensuring session continuity.

#### Overwriting Default Cookie Name

By default, RHOCP auto-generates the cookie name for ingress and route resources. However, troubleshooters can overwrite this default cookie name using the `annotate` command with either `kubectl` or `oc`. 

#### Example Usage

```bash
oc annotate ingress ingr-example ingress.kubernetes.io/affinity=cookie
oc annotate route route-example router.openshift.io/cookie_name=myapp
ROUTE_NAME=$(oc get route <route_name> -o jsonpath='{.spec.host}')
curl $ROUTE_NAME -k -c /tmp/cookie_jar
```

The cookie is passed back in response to the request and is saved to the `/tmp/cookie_jar` directory.

Embark on this journey of sticky sessions, as we configure session persistence to ensure uninterrupted user experiences within the mystical confines of the Openshift castle.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>