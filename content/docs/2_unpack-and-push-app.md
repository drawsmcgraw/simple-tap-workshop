# Unpack The Demo App and Push

## Unpack
Create a directory, named `workspace`. Place the demo app tarball in there and unpack it.

This project will be built by the platform. There is no need to build it.

## Push

Push the workload:
```sh
tanzu apps workload create tanzu-java-web-app \
  --local-path . \
  --source-image {{< param harbor_url >}}/tap-workshop/hello-tap \
  --type web \
  --label app.kuberenetes.io/part-of=tanzu-java-web-app \
  --label apps.tanzu.vmware.com/has-tests=true
```

The command is verbose for pedagogical reasons. During your day-to-day development, you will use a much shorter command involving a `workload.yaml` file. That file will look something like the file below:

```yaml
apiVersion: carto.run/v1alpha1
kind: Workload
metadata:
  name: tanzu-java-web-app
  labels:
    apps.tanzu.vmware.com/workload-type: web
    app.kubernetes.io/part-of: tanzu-java-web-app
spec:
  source:
    git:
      url: https://github.com/sample-accelerators/tanzu-java-web-app
      ref:
        branch: main
```


Now tail the workload to see it get built and deployed:
```sh
tanzu apps workload tail tanzu-java-web-app --since 10m --timestamp
```

## Profit
Congrats! You just built and deployed your first application! 

Fetch the URL to your application with:
```sh
tanzu apps workload get tanzu-java-web-app
```

Next, we'll look at how the platform can automatically scale your app to zero.
