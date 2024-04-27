# Unveiling the Secrets of Openshift: Data Extraction from configurations

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/blueprint2.jpg?raw=true" alt="data_extraction" width="300" height="300">
</div>

## Objective

Master the art of extracting data from YAML representations of resources within the Openshift castle, unveiling insights and unraveling complexities.

## Prerequisites

To embark on this journey of data extraction, you'll need:

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic familiarity with command-line interfaces (CLI) and Kubernetes concepts.

## Introduction

As we delve deeper into the depths of the Openshift castle, we uncover hidden treasures within the YAML representations of its resources. These data-rich files hold the key to understanding the inner workings of the castle's components, offering a glimpse into its architecture and functionality.

## Extracting Data from YAMLs

Unlock the potential of data extraction with commands designed to parse YAML representations into a tabular format:
```bash
oc get pods \
-o custom-columns=PodName:".metadata.name",\
ContainerName:"spec.containers[].name",\
Phase:"status.phase",\
IP:"status.podIP",\
Ports:"spec.containers[].ports[].containerPort"
```

## Format output with JSONPath

For formatted output, harness the power of JSONPath expressions:
```bash
oc get pods \
-o jsonpath='{range .items[]}{"Pod Name: "}{.metadata.name}
{"Container Names:"}{.spec.containers[].name}
{"Phase: "}{.status.phase}
{"IP: "}{.status.podIP}
{"Ports: "}{.spec.containers[].ports[].containerPort}
{"Pod Start Time: "}{.status.startTime}{"\n"}{end}'
```

Unlock the hidden insights within the YAML representations of Openshift resources, and empower yourself with the knowledge to navigate its intricate architecture with confidence.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>