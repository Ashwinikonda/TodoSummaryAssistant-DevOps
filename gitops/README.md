# GitOps Deployment Model

## GitOps Flow

1. Developer pushes application or Kubernetes configuration changes to GitHub.

2. Jenkins detects the Git change and runs the CI pipeline.

3. Jenkins builds and tests the application.

4. Jenkins builds Docker images and pushes versioned images to Docker Hub.

5. Jenkins does NOT directly deploy to Kubernetes.

6. Kubernetes deployment configuration is maintained in the GitOps directory.

7. A GitOps controller can monitor the Git repository and synchronize the desired state from Git to the Kubernetes cluster.

8. Kubernetes then runs the version defined in Git.

## Deployment Trigger

A deployment is triggered when the GitOps repository changes.

For example, when the image tag in the Kubernetes manifest is changed from:

    image: ashwiniskonda/todo-summary-backend:old-tag

to:

    image: ashwiniskonda/todo-summary-backend:new-tag

the GitOps controller detects the Git change and synchronizes Kubernetes with the new desired state.

## Rollback

Rollback is performed using Git.

If a new deployment causes a problem, the previous working Git commit can be restored or reverted.

The GitOps controller detects the reverted state and synchronizes Kubernetes back to the previous working version.

Therefore, Git acts as the source of truth for Kubernetes configuration.