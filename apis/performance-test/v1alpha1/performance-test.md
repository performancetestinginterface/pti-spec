# Traffic Access Control

**API Group:** performance.pti-spec.io

**API Version:** v1alpha1

This set of resources allows users to define a performance test for
applications. 

## Specification

### PerformanceTest


```yaml
kind: HTTPRouteGroup
metadata:
  name: the-routes
matches:
- name: metrics
  pathRegex: "/metrics"
  methods:
  - GET
- name: everything
  pathRegex: ".*"
  methods: ["*"]
```

For this definition, there are two routes: metrics and everything. It is a
common use case to restrict access to `/metrics` to only be scraped by
Prometheus. To define the target for this traffic, it takes a `TrafficTarget`.

```yaml
---
kind: TrafficTarget
metadata:
  name: path-specific
  namespace: default
destination:
  kind: ServiceAccount
  name: service-a
  namespace: default
  port: 8080
specs:
- kind: HTTPRouteGroup
  name: the-routes
  matches:
  - metrics
sources:
- kind: ServiceAccount
  name: prometheus
  namespace: default
```



## Example Implementation

The following implementation shows four services api, website, payment and
prometheus. It shows how it is possible to write fine grained TrafficTargets
which allow access to be controlled by route and source.