# Overview
This Kubernetes drone plugin can be used to upgrade a Kubernetes CronJob with a newer version of an image. This is equivalent to running the following kubectl command:

```
kubectl set image cronjob/smallworker worker=myorg/worker:1.0.1
```

> The CronJob must already created, this plugin will does not create a new CronJob and will error if it does not exist.

It is inspired by https://github.com/honestbee/drone-kubernetes

## Example Pipeline Configuration  

```yaml
pipeline:
  deploy:
    image: quay.io/kehindeadewusi/drone-k8s-cronjob
    kubernetes_server: https://kubernetes.company.org
    kubernetes_token: CXHVLJSDKJFS...
    namespace: app
    cronjob: smallworker
    repo: myorg/myrepo
    container: my-container
    tag: mytag
```

Deploying containers across several CronJobs. Make sure your container name in your manifest is the same for each pod.

```yaml
pipeline:
  deploy:
    image: quay.io/kehindeadewusi/drone-kubernetes
    cronjob: [ my-cronjob1, my-cronjob2 ]
    repo: myorg/myrepo
    container: my-container
    tag: mytag
```

Deploying multiple containers within the same CronJob.

```yaml
pipeline:
  deploy:
    image: quay.io/kehindeadewusi/drone-kubernetes
    cronjob: my-cronjob
    repo: myorg/myrepo
+   container: [ my-container-1, my-container-2 ]
    tag: mytag
```

## Parameter Reference


| Parameter         | Description                                                            |
| ----------------- | ---------------------------------------------------------------------- |
| container         | Container name (setup with the name option in the kubernetes manifest) |
| crontab           | Crontab name                                                           |
| kubernetes_server | Kubernetes API server URL                                              |
| kubernetes_token  | Kubernetes service account token                                       |
| namespace         | Kubernetes namespace                                                   |
| repo              | Image to update full name (with registry path)                         |
| tag               | Image tag                                                              |
|                   |                                                                        |
