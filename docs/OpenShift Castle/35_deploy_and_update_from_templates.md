# Deploying and Updating from Templates

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/templatesdeploy.jpg?raw=true" alt="deploy_applications" width="300" height="300">
</div>

## Objective

Learn how to deploy and update applications using Openshift templates.

## Prerequisites

- Access to an Openshift cluster or a terminal emulator connected to one.
- Basic knowledge of Kubernetes, YAML syntax, and Openshift CLI commands.

## Introduction

Welcome, noble custodian of the Openshift kingdom! As you navigate the realm of templates, you'll discover the art of deploying and updating applications seamlessly. By leveraging Openshift templates, you can transform parameterized blueprints into tangible resources and ensure your deployments are consistent and well-maintained. Embark on this journey to master the deployment and update of applications from templates, enhancing the stability and efficiency of your domain.

## Deploying Applications from Templates

### Transforming Templates into Resources

In the heart of your kingdom, the `oc process` command serves as the magical incantation that transforms templates into sets of related Kubernetes resource manifests. This command uses parameter values to shape the blueprint into a deployable form.

To override default values and create a resource manifest, use the following command:

```bash
oc process my-cache-service -o yaml \
-p TOTAL_CONTAINER_MEM=1024 \
-p APPLICATION_USER='cache-user' \
-p APPLICATION_PASSWORD='my-secret-password' \
> my-cache-service-manifest.yaml
```

This command is akin to tailoring a royal decree to fit the specific needs of your realm, adjusting parameters to ensure optimal performance.

### Using Parameter Files

For greater convenience and version control, save the parameters in a versioned file and apply it using the `--param-file` option:

```bash
oc process my-cache-service -o yaml \
--param-file=my-cache-service-params.env > my-cache-service-manifest.yaml
```

This approach is like keeping a detailed ledger in the royal archives, ensuring all adjustments and configurations are well-documented and easily retrievable.

### Direct Deployment

To skip the manifest generation and apply the resources directly to the cluster, use command piping:

```bash
oc process my-cache-service --param-file=my-cache-service-params.env | oc apply -f -
```

This method streamlines the deployment process, casting your spell directly onto the resources without intermediary steps, ensuring swift and efficient execution.

## Updating Applications from Templates

### Comparing Updates

Before updating resources, compare the results of the proposed update against the live resource using the `diff` command:

```bash
oc process my-cache-service -o yaml --param-file=my-cache-service-params-2.env | oc diff -f -
```

This step is like consulting the royal advisors to assess the impact of new decrees, ensuring that the proposed changes align with the kingdom's best interests.

### Applying Updates

Once verified, apply the updates by piping the commands:

```bash
oc process my-cache-service --param-file=my-cache-service-params-2.env | oc apply -f -
```

This command enacts the new configurations, updating the resources in your kingdom to reflect the latest adjustments, ensuring your realm remains well-maintained and up-to-date.

## Conclusion

Congratulations, esteemed steward of the Openshift kingdom! By mastering the deployment and updating of applications from templates, you ensure your resources are efficiently managed and consistently configured. Embrace the power of templates to transform and maintain your realm, ensuring stability and efficiency in all your deployments.

With these skills, you hold the key to a well-ordered and dynamic kingdom, where resources are deployed and updated with precision and ease. Your kingdom flourishes under your wise and vigilant guidance, as you expertly wield the power of Openshift templates to shape and enhance your domain.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>

