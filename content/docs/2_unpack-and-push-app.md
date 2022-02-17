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

The command is verbose for pedagogical reasons. During your day-to-day development, you will use a much shorter command as well as live debugging (a topic for a later time).

Now tail the workload to see it get built and deployed:
```sh
tanzu apps workload tail tanzu-java-web-app --since 10m --timestamp
```

The command you ran is just the CLI version of creating a `workload.yaml` file. The CLI will generate the workload and prompt you for confirmation. That file will look something like the file below:

```yaml
---
apiVersion: carto.run/v1alpha1
kind: Workload
metadata:
  labels:
    app.kuberenetes.io/part-of: tanzu-java-web-app
    apps.tanzu.vmware.com/has-tests: "true"
    apps.tanzu.vmware.com/workload-type: web
  name: tanzu-java-web-app
  namespace: drmalone
spec:
  source:
    image: harbor.tanzu.tacticalprogramming.com/tap-workshop/hello-tap:latest@sha256:e5b9a7c13aaa27dc6e307762d4c71208e7edb83c5ce14967fcccbf709d179205
```

Notice that the `spec.source` key is using the `image` parameter. That's because your previous command made an `imgpkg` artifact out of your code and pushed it to the container registry. That artifact is now the source of your code. The platform pulled down your code from that container registry, and put it into the Supply Chain responsible for building the app. More on supply chains later.

In a later section, we'll show how to use a git repo as the source of your code.


## Profit
Congrats! You just built and deployed your first application! 

Fetch the URL to your application with:
```sh
tanzu apps workload get tanzu-java-web-app
```

Past it into a browser (or `curl` it) and see your app live in production!

Next, we'll look at how the platform can automatically scale your app to zero.
