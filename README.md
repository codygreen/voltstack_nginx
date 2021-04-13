# Deploy NGINX Plus in a Volterra VoltStack

This demo will deploy NGINX Plus in a Volterra VoltStack via K8S manifest

## Download and Set KUBECONFIG variable

From VoltConsole, you need to create and download your Kubeconfig file. Check out the Volterra documentation for instructions:
https://www.volterra.io/docs/how-to/app-management/create-vk8s-obj

Once you've downloaded your Kubeconfig file, set the `KUBECONFIG` environment variable to point to this file:

```bash
export KUBECONFIG=ves_<your-namespace>_<your-vk8s>.yaml
```

## Set K8S secret with DockerHub credentials

You will need to create a DockerHub PAT for this step

```bash
kubectl create secret docker-registry regcred --docker-server=https://index.docker.io/v2/ --docker-username=<your-name> --docker-password=<your-pword> --docker-email=<your-email>
```

## Deploy NGINX Plus in VoltStack

Volterra uses VoltStack to create a virtual K8S cluster across all specified virtual sites. In this demo we will use kubectl to deploy out NGINX Plus instance from a private registry.

**Note**: You will need to change the `.spec.template.spec.containers.image` to point to your private DockerHub registry and application.

```bash
kubectl apply -f nginx_plus_manifest.yaml
```
