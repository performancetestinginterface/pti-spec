# Performance Test

**API Group:** performancetest.pti-spec.io

**API Version:** v1alpha1

This set of resources allows users to define a performance test for
applications. 

## Specification

### PerformanceTest

#### Runner
This resource is used to describe a runner. It is a simple runner configuration that allows the performance testing provider to define a pod spec.

```yaml
apiVersion: specs.pti-spec.io
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

#### PerformanceTest
This resource is used to describe a perofrmance test. It is a simple test configuration that allows the performance testing provider to define configure the full deployment spec with standard testing paramters.

```yaml
apiVersion: specs.pti-spec.io
kind: PerformanceTest
metadata:
  name: performance-test-for-foo-application
spec:
  runner:
    name: test-runner
    replicas: 1
    total-requests: 100
    queries-per-second-limit: 1
```  
## Out of Scope

* Passing of scripts via ConfigMaps - ConfigMaps are non-versionable entities and do not fit natually into the development flow in this manner. 