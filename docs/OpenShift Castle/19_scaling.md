# Scale Application

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/siege.jpg?raw=true" alt="scale_application" width="300" height="300">
</div>

## Objective

Learn how to scale applications in the mystical realms of Openshift to meet varying workload demands.

## Prerequisites

To embark on this journey of scaling applications, you'll need:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic understanding of Openshift concepts and command-line interfaces (CLI).

## Introduction

Welcome, valiant protector, to the realm of scaling the fortress within the enchanted confines of Openshift. Just as a fortress must adapt its defenses to withstand the onslaught of adversaries, so too must your applications be scaled to meet the ever-changing demands of your digital realm. Join us as we explore the methods of fortification and learn how to adapt to the shifting landscapes of workload demands.

## Scaling the Fortress

### Manually Adjusting Replicas: Rallying the Troops

In Openshift, troubleshooters can manually adjust the number of replicas for a deployment to scale the fortress up or down according to the intensity of the siege. This enables them to efficiently allocate resources and maintain performance under varying circumstances.

#### Example Usage

```bash
oc scale --replicas 5 deployment/fortress
```

Embark on this journey of scaling the fortress, as we wield the power to adapt and fortify our defenses within the ever-changing landscapes of Openshift.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>