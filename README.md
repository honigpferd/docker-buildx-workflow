# docker-buildx-workflow
a workflow to build multitarget docker images

## usage
reuse this github workflow with `.github/workflows/<my_workflow>.yaml`
```YAML
name: <myWorkflow>

on: <myTriggers>

jobs:
  <my-docker-buildx-workflow>:
    uses: honigpferd/docker-buildx-workflow/.github/workflows/docker-buildx.yml@v1
    permissions:
      contents: read
      packages: write
    with:
      platforms: 'linux/amd64,linux/arm64'    #  (default)
      registry: 'ghcr.io'                     #  (default)
      image_name: ${{ github.repository }}    #  (default)
      tags: |                                 #  (default)
        type=schedule
        type=ref,event=branch
        type=ref,event=pr
        type=semver,pattern={{version}}
        type=semver,pattern={{major}}.{{minor}}
        type=semver,pattern={{major}}
        type=sha

```
