# Logging In

When using TAP, everything happens in a Kubernetes cluster. Specifically, all of your activity as a developer will happen in a Kubernetes namespace. Before moving on with the workshop, we'll need to confirm that you have access to your k8s namespace.

There is a developer namespace set up for you on the Kubernetes cluster. After logging into your dev environment, you'll need to set the name of your developer namespace. After that, you can test connectivity.

```sh
# set developer namespace
export DEV_NAMESPACE='your-namespace'
kubectl -n $DEV_NAMESPACE get pods
```

To save some typing, you can use an alias so that all kubectl and tanzu commands use this namespace.

```sh
alias kubectl='kubectl -n $DEV_NAMESPACE'
alias tanzu='tanzu -n $DEV_NAMESPACE'
```

Confirm success by fetching a list of apps (we won't see any since we're starting out).

```sh
tanzu apps workload list
```

NOTE: For the remainder of this workshop, we will assume that you have this alias in place. All `kubectl` and `tanzu` commands will target your developer namespace.
