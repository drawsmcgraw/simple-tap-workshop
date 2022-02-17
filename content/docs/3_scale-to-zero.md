# Scaling to Zero
Because Cloud Native Runtime Service runs on top of Knative, your application, by default, will scale down to zero if it does not see any requests in a period of time. 

You can observe this by tailing the logs and waiting for output similar to the following:

```
+ tanzu-java-web-app-00001-deployment-788fc7b87-t4tmq › workload
+ tanzu-java-web-app-00001-deployment-788fc7b87-t4tmq › queue-proxy
unexpected error: container "queue-proxy" in pod "tanzu-java-web-app-00001-deployment-788fc7b87-t4tmq" is waiting to start: ContainerCreating
unexpected error: container "workload" in pod "tanzu-java-web-app-00001-deployment-788fc7b87-t4tmq" is waiting to start: ContainerCreating
- tanzu-java-web-app-00001-deployment-788fc7b87-t4tmq › queue-proxy
- tanzu-java-web-app-00001-deployment-788fc7b87-t4tmq › workload
+ tanzu-java-web-app-00001-deployment-788fc7b87-t4tmq › workload
+ tanzu-java-web-app-00001-deployment-788fc7b87-t4tmq › queue-proxy
```

After this happens, reload the app. There will be a small 'warmup' period when the app comes back up and you can see the app coming back up in the logs you're tailing. After a short moment, the app will return a response. 

It's worth noting that this behavior is only the default behavior and can be changed, if desired.


## Next Steps
That covers pushing code from a local workstation. Next, we'll achieve the same results, but by updating our code in a git repo instead.
