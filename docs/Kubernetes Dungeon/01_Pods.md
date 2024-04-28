# The Pod

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/k8s/dragonscientist.jpg?raw=true" alt="adv" width="300" height="300">
</div>

## Objective

Learn the basic configuration of a Kubernetes pod by observing a cute dragon pod.

## Storytime

In the mystical realm of Vitrua, there dwelled a revered scientist whose companion was a venerable dragon in the twilight of its existence. Determined to extend the dragon's waning years, the scientist delved into the arcane arts of longevity. Initially, he succeeded in encapsulating the essence of the dragon within a mesmerizing **image**, a tapestry of intricate **layers**. However, it was only when this image was ensconced within a **container**, a mystical orb, that true transformation occurred, imbuing the dragon with a vitality beyond its natural state.

The dragon was still sad, as it had troubles interacting with the external world from it's container, so the scientist had to find a solution to facilitate the dragon's interaction with the world outside its confines. Through relentless experimentation, he devised a remarkable exoskeleton using a deceptively simple engineering blueprint:

## Pod basic yaml 

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: dragon-pod
  labels:
    type: dragon-app
spec:
  containers:
  - name: dragon-container
    image: dragon-image:latest
    ports:
    - containerPort: 443
      protocol: TCP
```

## Components explanation

The scientist has made quite the simple but effective blueprint. Let's break down the YAML structure:

1. `apiVersion: v1`: This line specifies the API version being used to ensure compatibility with the cluster, which in this case is version 1 of the Kubernetes API. It's analogous to specifying the version of a software application.

2. `kind: Pod`: Here, a Kubernetes Pod is being defined. A Pod is the smallest deployable unit in Kubernetes, representing a single instance of a running process. This Pod likely encapsulates the environment for the dragon's consciousness and interaction.

3. `metadata`: This section provides metadata about the Pod, including its name and labels.

    - `name: dragon-pod`: This line specifies the name of the Pod, which is "dragon-pod". This name is how Kubernetes will refer to and manage this specific instance of the Pod.

    - `labels`: Labels are key-value pairs used to organize and select subsets of objects in Kubernetes. Here, the Pod is labeled with `type: dragon-app`, indicating that it belongs to a category of applications related to dragons.

4. `spec`: This section specifies the desired state for the Pod, including its containers and their configuration.

    - `containers`: This subsection defines the containers that should be launched within the Pod.

        - `name: dragon-container`: This line assigns a name to the container within the Pod. In this case, it's named "dragon-container", representing the vessel for the dragon's consciousness.

        - `image: dragon-image:latest`: Here, the image for the container is specified. The container will be created using the Docker image named "dragon-image" with the tag "latest". This image likely contains the necessary software and environment for the dragon's consciousness to operate within the container.

        - `ports`: This subsection specifies the ports that should be exposed by the container.

            - `- containerPort: 443`: This line indicates that the container should expose port 443, which is commonly used for HTTPS traffic. In the story, this port might be used for communication or interaction between the dragon and external systems.

            - `protocol: TCP`: This line specifies the protocol to be used for communication on the exposed port. In this case, it's TCP (Transmission Control Protocol), a common protocol used for reliable communication over networks.

Overall, this YAML file describes the configuration for a Kubernetes Pod named "dragon-pod", which contains a single container named "dragon-container" running the "dragon-image" Docker image. The container exposes port 443 for TCP communication, likely facilitating interactions between the dragon's consciousness and external systems in the Land of Vitrua.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>