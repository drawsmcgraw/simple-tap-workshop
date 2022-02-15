# Logging In

There is a developer namespace set up for you on the Kubernetes cluster. After logging into your dev environment, you'll need to set the name of your developer namespace. After that, you can test connectivity.

```
# set developer namespace
export DEV_NAMESPACE='your-namespace'
kubectl -n $DEV_NAMESPACE get pods
```

To save some typing, you can use an alias so that all kubectl commands use this namespace.

```
alias kubectl='kubectl -n $DEV_NAMESPACE'
alias tanzu='tanzu -n $DEV_NAMESPACE'
```

Confirm success by fetching a list of apps (we won't see any since we're starting out).

```
tanzu workload apps list
```

