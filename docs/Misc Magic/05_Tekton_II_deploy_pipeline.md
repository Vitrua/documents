# Tekton Pipelines simple deploy

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/misc/tessa2.jpg?raw=true" alt="tessa2" width="300" height="300">
</div>

## Objective
Learn how to use Tekton to build a container image and deploy it to a Kubernetes cluster.

## Storytime

In the magical land of Vitrua, Tessa the Sorceress had successfully summoned a friendly dragon using Tekton pipelines. Encouraged by her success, she decided to take her magical automation skills further. This time, she aimed to create a spell that would build a magical artifact (a container image) and deploy it to her enchanted Kubernetes cluster.

## The Advanced Spellcrafting Ritual

### Step 1: Define the Tasks

To build and deploy her magical artifact, Tessa needed to create two more tasks: one to build the container image and another to deploy it.

#### Task 1: Build Image

Tessa inscribed the following runes onto a magical scroll named `build-image-task.yaml`:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: build-image
spec:
  params:
    - name: IMAGE
      type: string
  steps:
    - name: build
      image: gcr.io/kaniko-project/executor:latest
      env:
        - name: DOCKER_CONFIG
          value: /tekton/home/.docker/
      script: |
        #!/bin/sh
        echo "Building image..."
        /kaniko/executor --dockerfile=Dockerfile --destination=$(params.IMAGE) --context=.
```
In the script to be executed, it uses Kaniko to build the image from a Dockerfile.

#### Task 2: Deploy to Kubernetes

Next, Tessa inscribed the following runes onto another scroll named `deploy-task.yaml`:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: deploy-to-k8s
spec:
  params:
    - name: IMAGE
      type: string
  steps:
    - name: deploy
      image: bitnami/kubectl:latest
      script: |
        #!/bin/sh
        echo "Deploying to Kubernetes..."
        kubectl set image deployment/my-app my-app=$(params.IMAGE)
```
In the script it uses kubectl to update the image of a Kubernetes deployment.

### Step 2: Define the Pipeline

Tessa needed to create a pipeline that would orchestrate these tasks in the correct order. She inscribed the following runes onto a scroll named `build-and-deploy-pipeline.yaml`:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Pipeline
metadata:
  name: build-and-deploy-pipeline
spec:
  params:
    - name: IMAGE
      type: string
  tasks:
    - name: build-image-task
      taskRef:
        name: build-image
      params:
        - name: IMAGE
          value: $(params.IMAGE)
    - name: deploy-to-k8s-task
      taskRef:
        name: deploy-to-k8s
      params:
        - name: IMAGE
          value: $(params.IMAGE)
      runAfter:
        - build-image-task
```

### Step 3: Create a PipelineRun

To initiate the building and deployment of her artifact, Tessa created a `PipelineRun`. She inscribed the following runes onto a scroll named `build-and-deploy-pipeline-run.yaml`:

```yaml
apiVersion: tekton.dev/v1beta1
kind: PipelineRun
metadata:
  name: build-and-deploy-pipeline-run
spec:
  pipelineRef:
    name: build-and-deploy-pipeline
  params:
    - name: IMAGE
      value: docker.io/your-repo/your-image:latest
```
Finally the parameters are passed to the pipeline, such as the image name.

### Step 4: Apply the Magical Scrolls

Tessa applied the magical scrolls to her Kubernetes cauldron to bring her pipeline to life:

```sh
kubectl apply -f build-image-task.yaml
kubectl apply -f deploy-task.yaml
kubectl apply -f build-and-deploy-pipeline.yaml
kubectl apply -f build-and-deploy-pipeline-run.yaml
```

### Step 5: View the PipelineRun Logs

To see the progress of her artifact creation and deployment, Tessa chanted the following spell to view the logs:

```sh
tkn pipelinerun logs build-and-deploy-pipeline-run -f
```

## The Grand Finale

With a sense of accomplishment, Tessa watched as her pipeline built the container image and deployed it to her Kubernetes cluster. The artifact, now deployed, was a testament to the power of Tekton and Tessa's advanced spellcrafting skills.

## Magical Tekton Commands Summary:

- `kubectl apply -f <file.yaml>`: Apply a YAML configuration to the Kubernetes cluster.
- `tkn pipelinerun logs <pipeline-run-name> -f`: View logs of a pipeline run.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>