# Earthly Buildkit Chart

This chart provides a Kubernetes deployment that implements a remote instance of `earthly/buildkitd`, as [described in the Earthly docs](https://docs.earthly.dev/ci-integration/remote-buildkit).

## Usage
_I haven't made this in to a proper Helm chart yet, so for now just clone it down and `helm install` it manually._

```bash
git clone git@github.com:RecordReplay/earthly-buildkit-chart.git
cd earthly-buildkit-chart
helm install buildkit .
```

