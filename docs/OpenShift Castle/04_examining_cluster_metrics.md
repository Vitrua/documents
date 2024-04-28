# Examine Cluster Metrics

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/measures.jpg?raw=true" alt="metrics" width="300" height="300">
</div>

## Objective

Examining cluster metrics, revealing the heartbeat of the operations of the Openshift castle.

## Prerequisites

To embark on this journey of exploration, you'll need:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic familiarity with command-line interfaces (CLI) and Kubernetes concepts.

## Introduction

As we journey further into the heart of the Openshift castle, we uncover the realm's hidden secrets through the examination of cluster metrics. These metrics serve as the pulse of the castle, offering glimpses into its inner workings and resource utilization.

## Examining Cluster Metrics

To peer into the total CPU usage of all pods within the cluster, our adventurers employ the following command:
```bash
oc adm top pods -A --sum
```
For a more focused inquiry into a single pod's CPU usage, they utilize the command:
```bash
oc adm top pods <pod_name> -n <namespace> --containers
```
## Metrics from interface

Within the stronghold's grand halls, adventurers find themselves drawn to the **Home** -> **Overview** section of the web interface, where the castle's metrics are displayed like ancient tapestries, meticulously sorted by resource utilization. Here, amidst the hustle and bustle of the castle's daily activities, they gain a fleeting glimpse of the main consumers within its walls, providing a quick overview of the kingdom's vitality.

Yet, for those intrepid souls yearning for deeper insights and exploration, a path awaits within the **Observe** -> **Metrics** section. Here, amidst the solemn grandeur of the castle's observatory, Prometheus queries can be executed like incantations, summoning forth insights from the depths of time. Through the arcane language of time-series graphs, adventurers unlock the secrets hidden within the castle's vast expanse of data and metrics.

Embark on this journey of discovery, as we unravel the mysteries concealed within the labyrinthine corridors of Openshift's castle, and illuminate the path to enlightenment for all who dare to venture forth.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>