# Limit Ranges in Namespace

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/limname.jpg?raw=true" alt="limname" width="300" height="300">
</div>

## Objective

Understand how to manage and enforce resource usage limits within namespaces using LimitRange objects in Kubernetes and OpenShift.

## Introduction

In the kingdom of OpenShift, just as there are rules and regulations to ensure that no guild or faction uses more resources than necessary, LimitRanges are set to enforce resource usage limits within namespaces. These limits ensure that all workloads operate efficiently, without overconsuming resources and disrupting the harmony of the digital kingdom.

## Limit Ranges

LimitRange objects define resource usage limits for workloads within a namespace. They are like the kingdom's laws that set boundaries on how much resources each guild (namespace) can use, ensuring fair and efficient resource distribution.

### Example Configuration

Here is an example of a `LimitRange` configuration:

```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: mem-limit-range
  namespace: default
spec:
  limits:
    - default:
        memory: 512Mi
      defaultRequest:
        memory: 256Mi
      type: Container
```

### Explanation

- **apiVersion**: Specifies the API version.
- **kind**: Defines the resource type, which is `LimitRange`.
- **metadata**: Contains metadata about the resource, such as its name and namespace.
- **spec**: Contains the specifications for the limit range.
  - **limits**: Defines the resource limits.
    - **default**: Specifies the default limits for containers.
    - **defaultRequest**: Specifies the default resource requests for containers.
    - **type**: Indicates the type of resource the limit applies to, such as `Container`.

### Additional Fields

- **max** and **min**: Specify the maximum and minimum values for both limits and requests.
- **maxLimitRequestRatio**: Controls the relationship between limits and requests.

Limit ranges can apply to various resources, including containers, pods, images, image streams, and persistent volume claims. However, they do not affect existing pods, much like new laws that only apply to future actions and not past deeds.

### Enforcing Limit Ranges

Even when a limit is not explicitly declared, the Kubernetes API server includes an admission controller that enforces limit ranges. This controller affects pod definitions but not deployments, stateful sets, or other workloads. It's akin to a royal enforcer ensuring that all new guild members adhere to the kingdom's laws from the moment they join.

## Updating Resource Limits

To update the CPU limit or add other resource specifications, you can use the `oc set resources` command. For example:

```bash
oc set resources deployment example --limits=cpu=new-cpu-limit
```

This command is like issuing a new decree that adjusts the resource usage for specific guilds within the kingdom.

### Handling Out-of-Range Requests

If you request CPU values outside the range defined by the `min` and `max` keys, Kubernetes will not create the pods and will log warnings. This is similar to the kingdom rejecting guild requests that exceed the allowed resource limits and issuing warnings to the guild leaders.

## Resource Quota Considerations

When doing a deployment rollout, the pods of both replica sets count towards the resource quota. If the quota is exceeded, the rollout will not complete. This ensures that resource allocation remains balanced, much like ensuring that no guild can monopolize the kingdom's resources during an expansion or new project.

## Conclusion

Managing namespace resources with LimitRange objects in OpenShift helps ensure fair and efficient resource usage across the digital kingdom. By setting clear boundaries and enforcing them through admission controllers, administrators can maintain harmony and prevent resource contention among workloads. Adjusting resource limits and handling out-of-range requests further ensures that all guilds (namespaces) operate within their allocated resources, preserving the kingdom's stability and prosperity.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>