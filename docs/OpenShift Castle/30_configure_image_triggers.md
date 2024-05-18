# Configuring Image Triggers

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/imagetriggers.jpg?raw=true" alt="image_triggers" width="300" height="300">
</div>

## Objective

Learn how to configure image triggers in Openshift to automate the rollout of new application versions when updated images become available.

## Prerequisites

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic knowledge of Openshift concepts and command-line interfaces (CLI).
- Familiarity with image streams and deployment objects.

## Introduction

Welcome back, vigilant guardian of the Openshift kingdom! In our previous journey, we discovered the secrets of image streams, the enchanted scrolls that guide your applications to stable and reproducible deployments. Now, we delve into the arcane art of configuring image triggers, the magical mechanism that ensures your deployments automatically update when new versions of images are available. Just as a castle's defenses must be ever-ready for new threats, your deployments must seamlessly incorporate the latest enhancements. Join us as we unravel the mysteries of image triggers and fortify your Openshift domain.

## Understanding Image Triggers

### The Magic of Image Triggers

In the enchanted Openshift realm, an image stream tag points to an immutable image, recording the SHA ID of the source image. When a new version of the image becomes available, the image stream tag can be updated to point to the new image. However, to ensure that deployment objects automatically roll out this new image, you must configure image triggers.

Think of image triggers as the castle's automatic alarms that notify the guards of any changes and prompt immediate action to update defenses. These triggers ensure that your applications are always running the most current and secure versions.

## Configuring Image Triggers

### Setting the Image Trigger

To configure an image trigger for a deployment object, use the `oc set triggers` command. This command is like casting a spell that binds the deployment to automatically update when the image stream tag is updated:

```bash
oc set triggers deployment/mykeycloak --from-image keycloak:20 --containers keycloak
```

This command sets up the trigger to update the deployment whenever the `keycloak:20` image stream tag is updated.

### Disabling and Enabling the Image Trigger

There may be times when you need to temporarily disable the image trigger. Use the `--manual` option to disable it, and the `--auto` option to re-enable it. This is akin to pausing and resuming the castle's alarms:

```bash
oc set triggers deployment/mykeycloak --manual --from-image keycloak:20 --containers keycloak
oc set triggers deployment/mykeycloak --auto --from-image keycloak:20 --containers keycloak
```

### Removing the Image Trigger

If you need to remove the triggers from all the containers in the deployment object, use the `--remove-all` option. This is like disarming all the castle's automatic alarms:

```bash
oc set triggers deployment/mykeycloak --remove-all
```

### Image Triggers and Rollouts

Another important detail is that when you use the `oc rollout undo` command, the image trigger gets disabled to prevent it from rolling out the newest image again. This ensures that your deployment reverts to the previous state without immediately updating to the latest image again:

```bash
oc rollout undo deployment/mykeycloak
```

For Openshift Deployment objects, this command works seamlessly. However, for Kubernetes deployment objects, the `rollout undo` command does not work the same way, and you need to manually revert the image stream tag.

### Aliasing Image Stream Tags

You can also create multiple image stream tags that point to the same image and visualize that both tags point to the same image. This is like giving different names to the same enchanted scroll, making it easier to manage and reference:

```bash
oc tag --alias keycloak:20.0.2 keycloak:20
oc describe is keycloak
```

## Conclusion

Congratulations, noble protector of the Openshift kingdom! By mastering the art of configuring image triggers, you ensure that your applications automatically update to incorporate the latest enhancements, maintaining their resilience and security. Just as a wise ruler maintains vigilant and responsive defenses, you too can safeguard your applications and ensure their continuous improvement within the Openshift domain.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>