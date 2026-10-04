# Failure and Rollback

## 1. A faulty version is deployed to production

If a new version has some issue after deployment, I would rollback to the previous working version.

Since the Kubernetes configuration is maintained in Git, I can revert the Git commit which introduced the faulty image/configuration. The GitOps process can then bring Kubernetes back to the previous state.

For example, if the new image is not working, I can change the image tag back to the previous working image tag and commit the change.

This helps to restore the application to a known working version.



## 2. Application crashes after deployment

Kubernetes checks the application using liveness and readiness probes.

If the application crashes, Kubernetes can restart the container. If the pod is not ready, Kubernetes will not send traffic to that pod.

The Deployment also maintains the required number of replicas, so Kubernetes can create a new pod if the existing pod fails.

I would also check the application logs and pod status to find the actual reason for the crash.



## 3. Jenkins is down

Jenkins is mainly used for the CI part of the pipeline, such as running tests and building Docker images.

If Jenkins is down, a new CI build will not run until Jenkins is available again. However, the already deployed application will continue running in Kubernetes.

The GitOps configuration is stored in Git, so Kubernetes deployment state is not dependent on Jenkins being continuously available.

Once Jenkins is restored, the pending code changes can be processed again.



## 4. Secrets are leaked

If a secret such as a database password, API key or webhook URL is leaked, I would first revoke or rotate the leaked secret.

Then I would create a new secret and update the application to use the new value.

I would also check Git history and make sure the secret is not stored in the repository. Secrets should be passed through Kubernetes Secrets or the CI/CD credential system instead of hardcoding them in code or configuration files.

If required, I would also review logs and access to check whether the leaked secret was used.



## 5. Kubernetes node fails

If a Kubernetes node fails, the pods running on that node become unavailable.

Kubernetes can schedule replacement pods on another available node, provided there is another suitable node and enough resources.

The Deployment maintains the desired number of replicas and Kubernetes works to bring the application back to the desired state.

I would check the node and pod status using Kubernetes commands and verify that the application is running normally after recovery.