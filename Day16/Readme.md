# Image Pull Policy in Kubernetes
Overview

In Kubernetes, the imagePullPolicy field of a container specification determines when the container runtime should pull (download) the container image from the image registry. This setting is critical for controlling container image freshness and optimizing cluster performance.
Image Pull Policy Options

Kubernetes supports the following values for imagePullPolicy:
1. Always

    Behavior: Pulls the image every time the pod starts.

    Use Case:

        Useful during active development.

        Ensures the latest version of the image is always used.

    Example:

    imagePullPolicy: Always

2. IfNotPresent

    Behavior: Pulls the image only if it is not already present on the node.

    Use Case:

        Best for stable images and reducing bandwidth usage.

    Example:

    imagePullPolicy: IfNotPresent

3. Never

    Behavior: Never pulls the image; only uses the local image.

    Use Case:

        For offline environments or when you manually preload images.

    Example:

    imagePullPolicy: Never

Default Behavior

If the imagePullPolicy is not explicitly specified, Kubernetes applies these defaults:

    If the image tag is :latest, the default is Always.

    For any other tag, the default is IfNotPresent.

Best Practices

    Use :latest tag with Always only for development/testing.

    Use versioned tags with IfNotPresent for predictable deployments.

    Avoid using Never unless you're managing image availability manually.

Example YAML
```
apiVersion: v1
kind: Pod
metadata:
  name: sample-pod
spec:
  containers:
  - name: sample-container
    image: myregistry/myimage:v1.0.0
    imagePullPolicy: IfNotPresent
```
### Troubleshooting

    If your pod fails with an image pull error, check:

        Network connectivity to the image registry.

        Image name and tag correctness.

        ImagePullSecrets (for private registries).

        The value of imagePullPolicy.

### Note: Endpoint ip to name resolution happens only inside pods, not from nodes. 