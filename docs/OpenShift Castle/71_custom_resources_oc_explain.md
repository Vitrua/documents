# Configuring Custom Resources with `oc explain`

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/oexplain.jpg?raw=true" alt="oexplain" width="300" height="300">
</div>


## Objective
Learn how to configure custom resources in your Kubernetes cluster using the `oc explain` command, especially when documentation is scarce.

## Prerequisites
- `oc` CLI installed.
- Connection to the Kubernetes cluster.
- Basic understanding of YAML and Kubernetes concepts.

## Storytime

In the grand Kingdom of Vitrua, nestled within the towering walls of the castle, lived a skilled knight named Sir Occulus. Sir Occulus was known far and wide for his mastery over the magical scrolls known as Custom Resources. These scrolls governed various aspects of the kingdom, from the bustling marketplaces to the serene gardens. However, among these scrolls there were uncommon ones like lokistack and clustertask, so the secrets of these scrolls were not always easy to decipher.

One day, Sir Occulus set out on a quest to uncover the mysteries of these custom resources, armed with a powerful artifact known as the `oc explain` command. This artifact allowed him to delve into the deepest corners of the scrolls, revealing their hidden fields and secrets.

## The Knight's Ritual:

1. **Unveiling the Pod Specification**:

    Sir Occulus began his journey by inspecting the common `pod.spec` scroll. With a wave of his enchanted blade, he invoked:
    ```bash
    oc explain pod.spec
    ```
    This revealed the structure and fields of the pod specification, guiding Sir Occulus in configuring the kingdom's battle formations.

2. **Deciphering the Lokistack Scroll**:

    The Lokistack scroll, uncommon one, essential for monitoring the kingdom's activities, was next on Sir Occulus' list. He chanted the following incantation:
    ```bash
    oc explain lokistack
    ```
    To explore deeper, he invoked:
    ```bash
    oc explain lokistack.spec.template.compactor
    ```

3. **Unveiling All Possible Fields**:

    For comprehensive knowledge, Sir Occulus used the powerful `--recursive` flag to reveal all potential fields of the uncommon Custertask scroll at once:
    ```bash
    oc explain clustertask --recursive
    ```

4. **Specifying the Scroll Version**:

    To ensure he was consulting the correct version of a scroll, Sir Occulus specified the API version using:
    ```bash
    oc explain clustertask --api-version=tekton.dev/v1beta1
    ```

5. **Consulting the Custom Resource Definition**:

    For an in-depth understanding of the schema, Sir Occulus referred to the 'Custom Resource Definition' of a scroll:
    ```bash
    oc get crd clustertasks.tekton.dev -o yaml
    ```

## The Grand Finale:

With the `oc explain` artifact, Sir Occulus demystified the custom resource scrolls of Vitrua, ensuring that the kingdom ran smoothly and efficiently. The knowledge he gained was shared with his fellow knights and scribes, safeguarding the prosperity of the castle.

## Enchanted Commands Summary:

- `oc explain pod.spec`: Reveal the structure and fields of the pod specification.
- `oc explain lokistack`: Decipher the Lokistack scroll.
- `oc explain lokistack.spec.template.compactor`: Explore deeper into the Lokistack scroll.
- `oc explain clustertask --recursive`: Unveil all possible fields at once.
- `oc explain clustertask --api-version=tekton.dev/v1beta1`: Specify the API version of a scroll.
- `oc get crd clustertasks.tekton.dev -o yaml`: Consult the Custom Resource Definition for detailed schema information.

Thus, Sir Occulus' tale of mastering custom resources became legend in the annals of the castle, guiding future knights and scholars in the art of Kubernetes configuration.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>