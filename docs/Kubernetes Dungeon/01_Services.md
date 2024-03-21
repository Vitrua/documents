# Services: ClusterIp, NodePort, LoadBalancer

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/k8s/adventurers.jpg?raw=true" alt="adv" width="300" height="300">
</div>

## Story time
Once upon a time, three intrepid souls roamed the land: Brave Ben, Resourceful Rina, and Fearless Fred. One fateful day, they set their sights on the legendary Cluster Castle, a fabled dungeon rumored to conceal secrets of immense power and knowledge.

Approaching the castle's entrance, they resolved to compete in their quest for the coveted treasures within. Each determined to claim the prized bounty first.

As they ventured forth, they diverged onto separate paths, destined for an unexpected encounter with three mystical guardians: ClusterIP, NodePort, and LoadBalancer.

Brave Ben, opting for a solitary journey into the depths, utilized his teleportation magic to navigate the labyrinthine tunnels. Amidst the maze, he encountered **ClusterIP**, a spectral guide. This entity ensured seamless communication within the dungeon's confines, shielding him from external interference. The aid of ClusterIP was akin to possessing an exclusive map of the tunnels, accessible only to those within its bounds.

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/k8s/spectre.jpg?raw=true" alt="spec" width="200" height="200">
</div>

Meanwhile, Resourceful Rina circled the castle walls until she stumbled upon a concealed door. Upon entering, she was greeted by **NodePort**, the stalwart guardian. NodePort facilitated external access to specific chambers within the dungeon, acting as a direct bridge between the interior and the outside world. It served as a key to unlock designated areas, granting entry to predetermined zones.

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/k8s/guardian.jpg?raw=true" alt="guard" width="200" height="200">
</div>

Finally Fearless Fred decided to boldly march through the main entrance, confronting a massive gate guarded by the imposing **LoadBalancer**. This formidable gatekeeper permitted numerous adventurers to access the dungeon's chambers. The LoadBalancer represented the necessity for a broader entry point, providing an accessible map to guide all who sought exploration within.

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/k8s/gatekeeper.jpg?raw=true" alt="gate" width="200" height="200">
</div>

Though taking different routes, ClusterIP, NodePort, and LoadBalancer guided the adventurers through the Cluster Castle, each ensuring access to its treasures while safeguarding its secrets with their protective measures. The three adventurers all emerged victorious, and returned laden with newfound knowledge and riches.

---

## Exercise: Managing Kubernetes Services - ClusterIP, NodePort, and LoadBalancer

**Objective:**
The objective of this exercise is to gain hands-on experience in managing different types of Kubernetes services: ClusterIP, NodePort, and LoadBalancer.

**Requirements:**
- Access to a Kubernetes cluster (locally installed or cloud-based)
- kubectl command-line tool installed and configured to communicate with the Kubernetes cluster

**Instructions:**
1. **Create a ClusterIP Service:**
    - Use either a YAML configuration file or the command line to create a ClusterIP service to connect an app to a port.

2. **Create a NodePort Service:**
    - Define a NodePort service to connect an app to a port, allowing external access by specifying a node port.

3. **Create a Basic LoadBalancer Service:**
    - Establish a basic LoadBalancer service to connect an app to a port.

4. **Confirm Service Creation:**
    - Verify that the services have been created correctly.

5. **Edit a Service:**
    - Modify or add a port, or link to a different element in at least one of the services.

6. **Clean Up Resources:**
    - Remove resources once the exercise is completed to prevent unnecessary costs or cluttering of the Kubernetes cluster.

**Example Solution Steps:**

Assuming you have a Kubernetes cluster set up and a sample application deployed named "my-app":

1. **Create ClusterIP Service:**
   ```bash
   kubectl create service clusterip my-app-clusterip --tcp=80:8080
   ```

2. **Create NodePort Service:**
   ```bash
   kubectl create service nodeport my-app-nodeport --tcp=80:8080 --node-port=30000
   ```

3. **Create LoadBalancer Service:**
   ```bash
   kubectl create service loadbalancer my-app-loadbalancer --tcp=80:8080
   ```

4. **Verify Service Creation:**
   ```bash
   kubectl get services
   ```

5. **Edit a Service:**
   ```bash
   kubectl edit svc my-app-clusterip
   ```

6. **Clean Up Resources:**
   ```bash
   kubectl delete service my-app-clusterip my-app-nodeport my-app-loadbalancer
   ```

These steps should provide a hands-on experience in managing various types of Kubernetes services and familiarize you with their configurations and functionalities.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true" alt="wiz" width="150" height="150">
  </a>
</div>