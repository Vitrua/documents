# Navigating the Openshift Realm: Exploring API Resources

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/blueprint1.jpg?raw=true" alt="discovery" width="300" height="300">
</div>

## Objective

Discover and explore the API resources available within Openshift to understand the landscape of its capabilities.

## Prerequisites

To embark on this journey of discovery, you'll need:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic familiarity with command-line interfaces (CLI) and Kubernetes concepts.

## Introduction

As we venture deeper into the heart of the Openshift castle, we uncover the API resources, the very fabric that defines the realm's architecture and functionality. These resources represent the essence of every component within the castle, guiding its operations and interactions.

## Viewing API Resources

The API resource objects serve as blueprints for the intended state of every entity in the cluster. Similar to their counterparts in the realm of Kubernetes, these commands offer insights into the castle's inner workings:
```bash
oc api-resources
```
You can refine and organize the results using additional flags:
```bash
oc api-resources --namespaced=true --api-group apps --sort-by name
```

## Openshift Main Resource Types

### BuildConfig: Architectural Blueprints
In the grand design of the Openshift castle, the BuildConfig stands as the architect's blueprint, defining the intricate process of constructing container images from source code stored in Git repositories. It is the cornerstone of continuous integration and delivery workflows, laying the foundation for innovation and evolution within Openshift projects.

### DeploymentConfig: Strategic Deployments
Within the fortified walls of Openshift, the DeploymentConfig serves as a strategic map, guiding the deployment and management of sets of containers within pods. With features encompassing scaling and deployment strategies, it orchestrates the movement of troops across the battlefield of the cluster. In Openshift 4.5, it yields to Deployment objects, heralding a new era of enhanced features and flexibility, yet its legacy remains ingrained in the castle's history.

### Routes: Pathways of Navigation
Like ancient pathways leading through the labyrinthine corridors of the Openshift castle, Routes are the DNS hostnames recognized by the Openshift router. They serve as the entry points for accessing applications and microservices, guiding travelers through the bustling streets and bustling squares of the cluster. With each route mapped and each journey embarked upon, they facilitate the seamless flow of traffic within Openshift's intricate network of pathways and passages.


Embark on this journey of exploration through the API resources of Openshift, unraveling its intricacies and unlocking its potential.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>