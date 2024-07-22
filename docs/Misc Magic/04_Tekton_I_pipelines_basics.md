# Tekton Pipelines basics

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/misc/tessa1.jpg?raw=true" alt="tessa1" width="300" height="300">
</div>

## Objective
Learn the basics components of Tekton pipelines.

## Prerequisites

- A terminal emulator connected to a Kubernetes cluster.

## Storytime

Once upon a time in the enchanted land of Vitrua, there was Tessa, a powerful sorceress using a magical system called Tekton.

One day, Tessa decided to create a new spell to summon a friendly dragon. She knew she needed to break this spell into two parts: one to conjure the dragon's form and another to bring the dragon to life. She would use Tekton to automate this process.

## The Spellcrafting Ritual

### Step 1: Install Tekton

Before Tessa could begin crafting her spells, she needed to ensure that Tekton was installed in her enchanted Kubernetes cauldron. She chanted the following incantation:

```sh
kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml
```

### Step 2: Define the Tasks

Tessa needed to create two tasks: one to conjure the dragon's form and another to bring the dragon to life.

#### Task 1: Conjure Dragon Form

Tessa inscribed the following runes onto a magical scroll named `conjure-dragon-task.yaml`:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: conjure-dragon
spec:
  steps:
    - name: conjure
      image: ubuntu
      script: |
        #!/bin/sh
        echo "Conjuring Dragon Form..."
```

#### Task 2: Bring Dragon to Life

Next, Tessa inscribed the following runes onto another scroll named `animate-dragon-task.yaml`:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: animate-dragon
spec:
  steps:
    - name: animate
      image: ubuntu
      script: |
        #!/bin/sh
        echo "Bringing Dragon to Life..."
```

### Step 3: Define the Pipeline

Tessa needed to create a pipeline that would orchestrate these tasks in the correct order. She inscribed the following runes onto a scroll named `dragon-pipeline.yaml`:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Pipeline
metadata:
  name: dragon-summoning-pipeline
spec:
  tasks:
    - name: conjure-dragon-task
      taskRef:
        name: conjure-dragon
    - name: animate-dragon-task
      taskRef:
        name: animate-dragon
      runAfter:
        - conjure-dragon-task
```

### Step 4: Create a PipelineRun

To summon the dragon, Tessa needed to create a `PipelineRun`. She inscribed the following runes onto a scroll named `dragon-pipeline-run.yaml`:

```yaml
apiVersion: tekton.dev/v1beta1
kind: PipelineRun
metadata:
  name: dragon-summoning-pipeline-run
spec:
  pipelineRef:
    name: dragon-summoning-pipeline
```

### Step 5: Apply the Magical Scrolls

Tessa applied the magical scrolls to her Kubernetes cauldron to bring her pipeline to life:

```sh
kubectl apply -f conjure-dragon-task.yaml
kubectl apply -f animate-dragon-task.yaml
kubectl apply -f dragon-pipeline.yaml
kubectl apply -f dragon-pipeline-run.yaml
```

### Step 6: View the PipelineRun Logs

To see the progress of her dragon summoning, Tessa chanted the following spell to view the logs:

```sh
tkn pipelinerun logs dragon-summoning-pipeline-run -f
```

## The Grand Finale

With a sense of accomplishment, Tessa watched as her pipeline conjured the dragon's form and brought it to life. The dragon, now summoned, was a testament to the power of Tekton and Tessa's spellcrafting skills.

## Tekton Commands Summary:

- `kubectl apply --filename <url>`: Install Tekton.
- `kubectl apply -f <file.yaml>`: Apply a YAML configuration to the Kubernetes cluster.
- `tkn pipelinerun logs <pipeline-run-name> -f`: View logs of a pipeline run.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>