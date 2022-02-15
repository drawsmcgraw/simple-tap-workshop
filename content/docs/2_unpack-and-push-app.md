# Unpack The Demo App and cf push

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

NOTE: The command is verbose for pedagogical reasons. During your day-to-day development, you will use a much shorter command involving a `workload.yaml` file.

Now tail the workload to see it get built and deployed:
```sh
tanzu apps workload tail tanzu-java-web-app --since 10m --timestamp
```

## Profit
Congrats! You just built and deployed your first application! See below for example output and an explanation of what just happened.

Fetch the URL to your application with:
```sh
tanzu apps workload get tanzu-java-web-app
```

That's pushing code from a local workstation. Next, we'll achieve the same results, but by updating our code in a git repo instead.
