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
Congrats! You just built and deployed your first application! 

Fetch the URL to your application with:
```sh
tanzu apps workload get tanzu-java-web-app
```

## Scale to Zero
Because Cloud Native Runtime Service runs on top of Knative, your application, by default, will scale down to zero if it does not see any requests in a period of time. 

You can observe this by tailing the logs and waiting for output similar to the following:

```
FILL IN THE BLANK
```

After this happens, reload the app. There will be a small 'warmup' period when the app comes back up and you can see the app coming back up in the logs you're tailing. After a short moment, the app will return a response. 

It's worth noting that this behavior is only the default behavior and can be changed, if desired.


## Next Steps
That's pushing code from a local workstation. Next, we'll achieve the same results, but by updating our code in a git repo instead.
