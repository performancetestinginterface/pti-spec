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
This resource is used to describe a performance test. It is a simple test configuration that allows the performance testing provider to define configure the full deployment spec with standard testing parameters.

```yaml
apiVersion: specs.pti-spec.io
kind: PerformanceTest
metadata:
  name: performance-test-for-foo-application
spec:
  runner:
    name: test-runner-for-foo-application
    replicas: 1
    total-requests: 100
    queries-per-second-limit: 1
``` 


#### PerformanceTestRun
This resource is to create a performance test run. It is a simple run configuration that allows the performance testing provider to create and run the test.

```yaml
apiVersion: specs.pti-spec.io
kind: PerformanceTestRun
metadata:
  name: performance-test-run-for-foo-application-as23fs
spec:
  performance-test: performance-test-for-foo-application
``` 


## Out of Scope

* Passing of scripts via ConfigMaps - ConfigMaps are non-versionable entities and do not fit naturally into the development flow in this manner. 