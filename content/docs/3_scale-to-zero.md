# Scaling to Zero
Because Cloud Native Runtime Service runs on top of Knative, your application, by default, will scale down to zero if it does not see any requests in a period of time. 

You can observe this by tailing the logs and waiting for output similar to the following:

```
FILL IN THE BLANK
```

After this happens, reload the app. There will be a small 'warmup' period when the app comes back up and you can see the app coming back up in the logs you're tailing. After a short moment, the app will return a response. 

It's worth noting that this behavior is only the default behavior and can be changed, if desired.


## Next Steps
That covers pushing code from a local workstation. Next, we'll achieve the same results, but by updating our code in a git repo instead.
