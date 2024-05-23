# Managing Templates

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/managetemplate.jpg?raw=true" alt="managing_templates" width="300" height="300">
</div>

## Objective

Learn how to manage Openshift templates by customizing default values and creating templates for specific usage targets, ensuring efficient resource configuration in production environments.

## Prerequisites

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic knowledge of Kubernetes, YAML syntax, and Openshift CLI commands.

## Introduction

Greetings, noble ruler of the Openshift kingdom! In your quest to maintain a well-ordered and efficient realm, mastering the management of templates is essential. By creating custom copies of templates and tailoring them to specific needs, you can ensure your resources are configured optimally for production workflows. Join us on this journey to refine your template management skills and enhance the stability and flexibility of your kingdom.

## Managing Templates

### Customizing Templates

In the heart of your kingdom, it's crucial to customize templates to meet the specific needs of your realm. Begin by making a custom copy of the template to adjust the default values. For example, to copy the `cache-service` template to a file, use the following command:

```bash
oc get template cache-service -o yaml -n openshift > my-cache-service.yaml
```

This action is akin to acquiring a blueprint from the royal archives, preparing it for modification to suit your unique requirements.

### Setting Up the Template

With the template copied, set it up by making the following adjustments:

1. **New Specific Name**: Assign a new name relative to the usage target, ensuring clarity and specificity in its purpose.
2. **Change Default Values**: Modify the default values of the parameters to align with your production needs.
3. **Remove Namespace Field**: Eliminate the namespace field to allow the template to be used in any project.

These steps ensure your template is finely tuned, ready to serve the distinct needs of your kingdom.

### Uploading the Template

Once customized, you can upload the template to the current project with the following command:

```bash
oc create -f my-cache-service.yaml
```

This command is like inscribing your newly crafted decree into the royal records, making it available for deployment.

Alternatively, to upload the template to a different project, use the `-n` option:

```bash
oc create -f my-cache-service.yaml -n another-project
```

Remember, this command creates the template but does not deploy the resources. It's akin to placing the blueprint in the hands of your engineers, ready for use when the time comes.

## Conclusion

Congratulations, esteemed custodian of the Openshift kingdom! By mastering the art of managing templates, you ensure your resources are configured optimally and tailored to the specific needs of your production environments. Embrace this power to create, customize, and manage templates, enhancing the efficiency and stability of your deployments.

With these skills, you hold the key to a well-ordered and dynamic kingdom, where resources are finely tuned and readily available for deployment. Your kingdom flourishes under your wise and vigilant guidance, as you expertly wield the power of Openshift templates to shape and enhance your domain.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>