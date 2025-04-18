## List of issues faced during the integration of microservice yaml files into the AKS clusters:

## 1. Pods status with "CrashLoopBackOff" for most of the microservices.

![CrashLoopBackOff Issue](https://github.com/Saikarthick07/bestbuy-deploymentfiles/blob/main/assets/CrashLoopBackOff.png)
The following pods are in a CrashLoopBackOff status:

- ai-service-5c4b957694-qd29c
- makeline-service-698dfdfb5c-drjl
- order-service-64f5b7487b-h6857
- product-service-574d5bfb5f-mw7
- store-admin-78f5994b4f-q9vjp

CrashLoopBackOff indicates that these pods are failing to start properly and are continuously crashing. This can be caused by various issues like:

- Incorrect configuration or environment variables.
- Missing or incorrect dependencies (like a database or external service).
- A misconfiguration in the container image or entry point.
- Insufficient resources (memory, CPU).
- Application errors in the code causing it to exit or crash.

## Steps to Troubleshoot:

Check Pod Logs:

- You can view the logs of the crashing pods to gather more details on the error causing them to crash.
- Use the following command to view the logs:
  "kubectl logs <pod-name> -n default"

(base) saikarthick@SAIs-MacBook-Air DeploymentFiles % kubectl logs pod/makeline-service-698dfdb5c-drjlb -n default

exec ./main: exec format error

## Possible Causes and Solutions:

- Incorrect Architecture (ARM vs. x86):
If you built the Docker image on a different architecture (e.g., ARM on a Mac) and are trying to run it on a different architecture (e.g., x86 on a Kubernetes cluster), this can lead to an exec format error.

- Solution: Ensure that the Docker image is built for the correct architecture. If you are using an ARM-based machine like a Mac with Apple Silicon (M1/M2), you need to ensure that the Docker image is built for both ARM and x86 architectures, or specifically for x86 if your Kubernetes cluster uses that architecture.

## Steps to Enable Multi-Platform Builds with docker-container Driver:

- Create a new builder using docker-container: Run the following command to create a new builder with the docker-container driver:
  "docker buildx create --use --driver docker-container"
  
- Verify the Builder: After creating the new builder, run this command to verify the active builder and its platforms:
  "docker buildx ls"
  You should see the docker-container driver listed as the active builder.

- Run the Multi-Platform Build Command: Now that you've switched to the docker-container driver, run the multi-platform build command again:
  "docker buildx build --platform linux/amd64,linux/arm64 -t <Docker-Hub-Username>/bestbuy-makeline-service:latest ."
  This should allow you to successfully build the Docker image for multiple platforms.

- Ensure you switch the directory to the affected microservices, and try to re-build the docker images using the Multi-Platform build command.


- Once created with the multi-platform docker build, pull the docker image into your local repository.






