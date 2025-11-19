# NeuVector – GitHub Action

This GitHub Action installs or upgrades **NeuVector** in a Kubernetes cluster.  

---

## What This Action Does

- Adds the NeuVector Helm repo
- Ensures the namespace exists
- Installs or upgrades NeuVector using Helm
- Allows specifying NeuVector product version (`tag`)

---

## Inputs

| Name | Required | Default | Description |
|------|----------|----------|-------------|
| `Namespace` | No | `neuvector` | Kubernetes namespace to install NeuVector |
| `HelmRepo` | No | `https://neuvector.github.io/neuvector-helm/` | NeuVector Helm repo |
| `RepoName` | No | `neuvector` | Alias name for Helm repo |
| `ChartName` | No | `neuvector/core` | Helm chart to install |
| `Version` | No | `""` | Product version (`--set tag=<version>`) |

---

## Example Usage

Create `.github/workflows/neuvector-install.yml`:

```yaml
name: Install NeuVector

on:
  workflow_dispatch:

jobs:
  neuvector:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Set Kubernetes Context
        uses: azure/k8s-set-context@v4
        with:
          method: kubeconfig
          kubeconfig: ${{ secrets.KUBECONFIG }}

      - name: Install NeuVector
        uses: your-org/neuvector-action@v1
```
## Example: optional inputs

Install a specific version:

```yaml
with:
  Version: "5.4.2"
```

Install into a different namespace:
```yaml
with:
    Namespace: "security"
```
