# Security Scans

The pipeline we've been using has been running scans on the containers that get built for us. Let's explore some of the artifacts that it generated.

## Set Up Environment

There are some environment variables that need to be created. Copy/Paste the following:

```sh
export METADATA_STORE_ACCESS_TOKEN=$(kubectl get secrets -n metadata-store -o jsonpath="{.items[?(@.metadata.annotations['kubernetes\.io/service-account\.name']=='metadata-store-read-write-client')].data.token}" | base64 -d)

export INGRESS_DOMAIN={{< param system_domain >}}

insight config set-target https://metadata-store.${INGRESS_DOMAIN} --access-token=$METADATA_STORE_ACCESS_TOKEN

export EXAMPLE_DIGEST=$(kubectl get kservice tanzu-java-web-app -o jsonpath='{.spec.template.spec.containers[0].image}' | awk -F @ '{ print $2 }')
```

Note: `insight` is a CLI we'll use to query the security metadata store.

## Query

Let's fetch an image scan:

```sh
insight image get --digest $EXAMPLE_DIGEST --format json
```

And we can also fetch a CVE scan. We can even grep through this output to quickly confirm/deny if we have any high level CVEs.

```sh
insight image vulnerabilities --digest $EXAMPLE_DIGEST --format json
```

Imagine the possibilities when we create pipelines that have machine-readable security artifacts we can make available to our Security team.
