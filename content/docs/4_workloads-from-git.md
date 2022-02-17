# Deploying Workloads From Git

Workloads can come from git repositories. In this section, we'll create a new workload from an existing git repo and observe the platform building/deploying the application.

## Delete the Previous Workload

To keep things simple, let's delete the old workload.

```sh
tanzu apps workload delete tanzu-java-web-app
```

## Create the Workload and Observe

```sh
tanzu apps workload create tanzu-java-web-app \
  --git-repo https://gitlab.com/drawsmcgraw/hello-tap \
  --git-branch master \
  --type web \
  --label app.kuberenetes.io/part-of=tanzu-java-web-app \
  --label apps.tanzu.vmware.com/has-tests=true
```

Notice that this time, the `source` in the workload is a git repo:

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
    git:
      ref:
        branch: master
      url: https://gitlab.com/drawsmcgraw/hello-tap
```

As before, tail the workload to see it get built and deployed:
```sh
tanzu apps workload tail tanzu-java-web-app --since 10m --timestamp
```

Also as before, fetch the URL to your application with:
```sh
tanzu apps workload get tanzu-java-web-app
```

After observing the application, tail the logs again. With the tailing window still active, make a change to the app and create a new commit in the git repo. After pushing the commit, the platform will detect this and begin building/deploying the new version of the application.
