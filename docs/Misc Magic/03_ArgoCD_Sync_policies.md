# The ArgoCD Sync Policies

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/misc/argasync.jpg?raw=true" alt="argasync" width="300" height="300">
</div>

## Objective
Learn how to configure and utilize various sync policies in ArgoCD for automated and manual synchronization of Kubernetes resources.

## Storytime

In the magical realm of Synkronia, there lived a wise sorceress named Arga. Arga was the guardian of the enchanted forests, where every plant and creature thrived in perfect harmony. Her secret? A mystical scroll called ArgoCD, which allowed her to synchronize the elements of her realm seamlessly.

One day, Arga discovered that the balance of the forest was threatened by dark forces. She needed to ensure that every part of the forest could heal and adjust automatically to maintain harmony. This is when she turned to the powerful spells inscribed in her ArgoCD scroll, known as sync policies.

## The Spellbinding Ritual:

1. **Automatic Pruning**:

    Arga decided that any out-of-place or unnecessary elements should be automatically pruned to maintain the forest's balance.
    ```
    spec:
      syncPolicy:
        automated:
          prune: true
    ```

    This spell ensures that any resources no longer needed are removed automatically.

2. **Automatic Pruning with Allow-Empty**:

    Sometimes, the forest might have areas that temporarily have no elements. Arga used a special spell to allow empty spaces without causing alarms.
    ```
    spec:
      syncPolicy:
        automated:
          prune: true
          allowEmpty: true
    ```

3. **Automatic Self-Healing**:

    To protect the forest from sudden disturbances, Arga enchanted it with a self-healing spell, ensuring it could repair itself.
    ```
    spec:
      syncPolicy:
        automated:
          selfHeal: true
    ```

4. **No Prune Resources**:

    Certain ancient trees and sacred groves should never be pruned. Arga marked these with a protective spell.
    ```
    metadata:
      annotations:
        argocd.argoproj.io/sync-options: Prune=false
    ```

5. **Disable Kubectl Validation**:

    For unique and rare plants that kubectl might not recognize, Arga bypassed the standard validation checks.
    ```
    metadata:
      annotations:
        argocd.argoproj.io/sync-options: Validate=false
    ```

6. **Skip Dry Run for New Custom Resource Types**:

    When introducing new magical creatures, Arga skipped the dry run to allow smooth integration.
    ```
    metadata:
      annotations:
        argocd.argoproj.io/sync-options: SkipDryRunOnMissingResource=true
    ```

7. **No Resource Deletion**:

    To safeguard critical elements, Arga ensured they would never be deleted.
    ```
    metadata:
      annotations:
        argocd.argoproj.io/sync-options: Delete=false
    ```

8. **Selective Sync**:

    Sometimes, only specific areas needed updating. Arga cast a spell to apply changes selectively.
    ```
    apiVersion: argoproj.io/v1alpha1
    kind: Application
    spec:
      syncPolicy:
        syncOptions:
        - ApplyOutOfSyncOnly=true
    ```

9. **Resources Prune Deletion Propagation Policy**:

    For resources that needed orderly removal, Arga used a specific propagation policy.
    ```
    apiVersion: argoproj.io/v1alpha1
    kind: Application
    spec:
      syncPolicy:
        syncOptions:
        - PrunePropagationPolicy=foreground
    ```

10. **Prune Last**:

    Arga ensured that pruning was the last step in the synchronization process.
    ```
    apiVersion: argoproj.io/v1alpha1
    kind: Application
    spec:
      syncPolicy:
        syncOptions:
        - PruneLast=true
    ```

11. **Replace Resource Instead of Applying Changes**:

    For completely renewing an element, Arga replaced it entirely rather than just applying changes.
    ```
    apiVersion: argoproj.io/v1alpha1
    kind: Application
    spec:
      syncPolicy:
        syncOptions:
        - Replace=true
    ```

12. **Force Sync**:

    To enforce immediate synchronization regardless of conflicts, Arga used a forceful incantation.
    ```
    metadata:
      annotations:
        argocd.argoproj.io/sync-options: Force=true,Replace=true
    ```

13. **Server-Side Apply**:

    Arga applied changes server-side for a more controlled and efficient synchronization.
    ```
    apiVersion: argoproj.io/v1alpha1
    kind: Application
    spec:
      syncPolicy:
        syncOptions:
        - ServerSideApply=true
    ```

14. **Fail the Sync if a Shared Resource is Found**:

    To prevent conflicts, Arga ensured the sync would fail if it detected resources shared by multiple spells.
    ```
    apiVersion: argoproj.io/v1alpha1
    kind: Application
    spec:
      syncPolicy:
        syncOptions:
        - FailOnSharedResource=true
    ```

15. **Respect Ignore Differences Configs**:

    Arga respected the differences specified for certain resources, ensuring harmony.
    ```
    apiVersion: argoproj.io/v1alpha1
    kind: Application
    spec:

      ignoreDifferences:
      - group: "apps"
        kind: "Deployment"
        jsonPointers:
        - /spec/replicas

      syncPolicy:
        syncOptions:
        - RespectIgnoreDifferences=true
    ```

16. **Create Namespace**:

    When a new habitat was needed, Arga created a namespace for it.
    ```
    apiVersion: argoproj.io/v1alpha1
    kind: Application
    metadata:
      namespace: argocd
    spec:
      destination:
        server: https://kubernetes.default.svc
        namespace: some-namespace
      syncPolicy:
        syncOptions:
        - CreateNamespace=true
    ```

17. **Namespace Metadata**:

    Arga also added specific labels and annotations to new namespaces for better management.
    ```
    apiVersion: argoproj.io/v1alpha1
    kind: Application
    metadata:
      namespace: test
    spec:
      syncPolicy:
        managedNamespaceMetadata:
          labels: # The labels to set on the application namespace
            any: label
            you: like
          annotations: # The annotations to set on the application namespace
            the: same
            applies: for
            annotations: on-the-namespace
        syncOptions:
        - CreateNamespace=true
    ```

## The Grand Finale:

With the ArgoCD scroll, Arga ensured the enchanted forest of Synkronia remained in perfect balance. The magical sync policies allowed the forest to heal, prune, and adjust itself, safeguarding it from dark forces. And so, the wisdom of Arga's spells was passed down through generations, ensuring that the magic of synchronization kept the realm thriving.

## Enchanted ArgoCD Sync Commands Summary:

- `spec: syncPolicy: automated: prune: true`: Enable automatic pruning.
- `spec: syncPolicy: automated: prune: true, allowEmpty: true`: Allow empty spaces.
- `spec: syncPolicy: automated: selfHeal: true`: Enable automatic self-healing.
- `metadata: annotations: argocd.argoproj.io/sync-options: Prune=false`: Protect resources from pruning.
- `metadata: annotations: argocd.argoproj.io/sync-options: Validate=false`: Disable kubectl validation.
- `metadata: annotations: argocd.argoproj.io/sync-options: SkipDryRunOnMissingResource=true`: Skip dry run for new custom resource types.
- `metadata: annotations: argocd.argoproj.io/sync-options: Delete=false`: Prevent resource deletion.
- `spec: syncPolicy: syncOptions: - ApplyOutOfSyncOnly=true`: Apply changes selectively.
- `spec: syncPolicy: syncOptions: - PrunePropagationPolicy=foreground`: Set prune propagation policy.
- `spec: syncPolicy: syncOptions: - PruneLast=true`: Prune resources last.
- `spec: syncPolicy: syncOptions: - Replace=true`: Replace resource instead of applying changes.
- `metadata: annotations: argocd.argoproj.io/sync-options: Force=true,Replace=true`: Force sync.
- `spec: syncPolicy: syncOptions: - ServerSideApply=true`: Server-side apply.
- `spec: syncPolicy: syncOptions: - FailOnSharedResource=true`: Fail sync on shared resource.
- `spec: ignoreDifferences: - group: "apps" kind: "Deployment" jsonPointers: - /spec/replicas`: Respect ignore differences.
- `spec: destination: server: https://kubernetes.default.svc namespace: some-namespace syncPolicy: syncOptions: - CreateNamespace=true`: Create namespace.
- `spec: syncPolicy: managedNamespaceMetadata: labels: any: label you: like annotations: the: same applies: for annotations: on-the-namespace`: Set namespace metadata.

Thus, the tale of Arga the Enchanted ArgoCD Sync Sorceress became a legend in Synkronia, inspiring future generations to master the art of synchronization and maintain the magical harmony of their realms.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>