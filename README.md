# TAP Workshop

## Building

To generate this workshop you'll need [Hugo](https://gohugo.io/) installed.

Once that's installed cd into the root of the project and run this:


Create a new file called `config.yml` with the following content, replacing `pivotal.io` with the appropriate domain name:

```
params:
  system_domain: pivotal.io
  use_packaged_cli: true
```

Then to use the live server on [http://localhost:1313](http://localhost:1313)
```
hugo --config ./config.yml,./config.toml server
```

To generate HTML output
```
hugo --config ./config.yml,./config.toml
```

