# Bundler
This generates an archive of Docker images for each Helm repository listed in the script.

### Prequisities
- jq      see [docs](https://mikefarah.gitbook.io/yq/) for instructions on installation for your platform
- Bash 5+
- yq      see [docs](https://stedolan.github.io/jq/download/) for instruction on installation for your platform
- gnu-sed brew install gnu-sed

### Usage
```
  Usage: bundle [options]
    -p     Prints a listing of helm packages
    -a     Builds an archive for each helm package
    -f     Import Bundle archive and push to registry. Requires a registry using -r option
    -r     Docker registry and port (default value is localhost:5000)
```

### Generate an archive
```
./bundler -a
```

### Import an archive into a private registry
This automatically tags all the images in the archive and pushes all the containers to the registry references.
```
./bundler -f bundles/gloo-mesh-enterprise.tar -r private.registry.comL:5000
``` 

### Add a Helm Repository
1. Add the chart to the packages variable.
```
packages=(
  "gloo-mesh-enterprise/gloo-mesh-enterprise:2.2.6"
  "istio/istiod:1.17.1"
  "istio-operator:1.17.1"
)
```
2. Add the Helm repository reference to repos.
```
declare -A repos=(
  ["gloo"]="https://storage.googleapis.com/solo-public-helm"
  ["glooe"]="https://storage.googleapis.com/gloo-ee-helm"
  ["gloo-mesh-enterprise"]="https://storage.googleapis.com/gloo-mesh-enterprise/gloo-mesh-enterprise"
  ["gloo-mesh-agent"]="https://storage.googleapis.com/gloo-mesh-enterprise/gloo-mesh-agent"
  ["istio"]="https://istio-release.storage.googleapis.com/charts"
  ["istio-operator"]="istio-1.17.1/manifests/charts/istio-operator"
)
```
