# Earthly Buildkit Chart

This chart provides a Kubernetes deployment that implements a remote instance of `earthly/buildkitd`, as [described in the Earthly docs](https://docs.earthly.dev/ci-integration/remote-buildkit).

## Installation
_I haven't made this in to a proper Helm chart yet, so for now just clone it down and `helm install` it manually._

```bash
git clone git@github.com:RecordReplay/earthly-buildkit-chart.git
cd earthly-buildkit-chart
helm install buildkit .
```

## Values
Here are some useful values in `values.yaml` that can be configured for this chart:

| Key      | Description |
| ----------- | ----------- |
| `replicaCount` | How many pods to run.        |
| `image` | Which image to run. By default is set to the latest `earthly/buildkitd` release.|
| `autoscaling` | Configuration options for a [horizontal pod autoscaler](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/).|


## Caveats
Currently this chart runs as a stateless deployment. This presents two challenges:

1) If the pods restart for any reason, you lose all cached layers, meaning that if you re-run a build it would suddenly be slower.
2) News pods also don't share any cache with existing pods, meaning that users can have an unevent experience where some builds are faster than others depending on which pod is servicing their request.

In the future it would be better to use a stateful set and a persistent volume to get around these issues. For now I find that this is good enough, but PRs welcome. :)