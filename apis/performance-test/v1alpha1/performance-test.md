# Traffic Access Control

**API Group:** performancetest.pti-spec.io

**API Version:** v1alpha1

This set of resources allows users to define a performance test for
applications. 

## Specification

### PerformanceTest


```yaml
kind: Runner
metadata:
  name: test-runner-for-foo-application
spec:
  image: <custom-image>
  metadata:
    labels:
      cool-label: foo
    annotations:
      cool-annotation: bar
  resources:
    limits:
      cpu: 200m
      memory: 1000mi
    requests:
      cpu: 100m
      memory: 500Mi
```

```yaml
kind: PerformanceTest
metadata:
  name: performance-test-for-foo-application
spec:
  runner:
    name: test-runner
    replicas: 1
    requests: 100
    queries-per-second: 1
```


## Example Implementation

The following implementation shows four services api, website, payment and
prometheus. It shows how it is possible to write fine grained TrafficTargets
which allow access to be controlled by route and source.