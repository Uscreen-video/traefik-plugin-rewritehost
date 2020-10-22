# Rewrite Host

Rewrite host is a middleware plugin for [Traefik](https://traefik.io) which extracts host and put it to specified header.

## Configuration

### Static 

```toml
[pilot]
  token = "xxxx"

[experimental.plugins.rewritehost]
  modulename = "github.com/Uscreen-video/traefik-plugin-rewritehost"
  version = "v0.0.1"
```


### Dynamic

To configure the Rewrite Host plugin you should create a [middleware](https://docs.traefik.io/middlewares/overview/) in your dynamic configuration as explained [here](https://docs.traefik.io/middlewares/overview/). The following example creates and uses the rewritehost middleware plugin to create a new header with extracted data from host.

```
[http]
  [http.routers]
    [http.routers.my-router]
      rule = "Host(`localhost`)"
      service = "my-service"
      middlewares = ["rewritehost"]

  [http.services]
    [http.services.my-service.loadBalancer]
      [[http.services.my-service.loadBalancer.servers]]
        url = "http://127.0.0.1"

  [http.middlewares]
    [http.middlewares.rewritehost.plugin.dev]
      create    = "X-Origin-Domain"    //required

```

