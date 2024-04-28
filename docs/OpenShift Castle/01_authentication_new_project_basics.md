# Authentication, new project and basic commands

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/incisions.jpg?raw=true" alt="inscription" width="300" height="300">
</div>

## Objective

Learn how to authenticate, create new projects, and some basic commands in Openshift. Enter the Openshift Castle.

## Prerequisites

To embark on this adventure, you'll need:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic familiarity with command-line interfaces (CLI) and Kubernetes concepts.

## Introduction

In the vast landscape of the digital realm, where clusters of containers flourish like bustling kingdoms, there lies the imposing fortress of Openshift. Built upon the foundation of Kubernetes, this castle stands as a bastion of security and scalability, protecting its treasures with unwavering vigilance.

Our hero, a brave adventurer seeking knowledge and mastery, stands before the gates of Openshift. The castle looms above, its architecture intricate and imposing, a testament to the power it holds within.

## Authentication Gates

Before venturing forth, our hero must authenticate at the castle gates. With the `oc login` command, he present their credentials:
```bash
oc login <cluster-url>
```

## Forging New Projects

A strange sensation courses through our hero's veins as they enter the castle, as if the fortress were under their command. The first thing noticed is the multitude of different wings within the castle, each isolated from the others. With newfound powers, our hero invokes the creation of a new project to carve out a new realm:
```bash
oc new project <my-app>
```

## Commanding the Castle

Adorning the walls are inscriptions in a mysterious language. Armed with the knowledge of oc commands, our hero delves deeper into the castle's inner workings:
```bash
oc cluster-info
oc api-versions
oc get clusteroperator
oc get pod
oc get pod <pod_name>
oc get pod <pod_name> -o yaml
oc get pod <pod_name> -o json
oc get deploy <deploy_name> -o wide
oc get all
oc describe <resource_type> <resource_name>
oc explain <jsonpath_identifier>
oc explain <jsonpath_identifier> --recursive
oc create -f <pod.yaml>
oc status --suggest
oc delete <resource_type> <resource_name>
```
For instance:
```bash
oc explain pods.spec.containers.resources
```
These commands unveil the secrets of the castle's infrastructure and its inhabitants.

To make these commands influence a different wing of the castle, than the one where he is in that moment, our hero needs to add the option `--namespace` or `-n` to the instruction:
```bash
oc get pod -n <namespace>
```

## Token of Entry - OAuth

For those who seek passage via OAuth, the castle offers tokens of entry:
```bash
oc login --token=sha256-BW...fE2 --server=https://api.eg.vitrua.top:6443
```
These tokens grant access to the castle's inner sanctums.

## Conclusion

And thus, the hero took his first steps inside the castle.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>