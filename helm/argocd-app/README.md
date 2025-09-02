# argocd-app Helm Chart

This chart creates an Argo CD AppProject and Application.

## Install

```bash
helm install my-argocd-app ./helm/argocd-app
```

## Values

- **project.enabled**: create AppProject (default true)
- **project.name**: project name
- **project.namespace**: Argo CD namespace
- **project.sourceRepos**: allowed repo URLs (default `*`)
- **project.destinations**: allowed destinations

- **application.enabled**: create Application (default true)
- **application.name**: application name
- **application.namespace**: Argo CD namespace
- **application.project**: project to bind to
- **application.source.repoURL**: Git repo URL
- **application.source.targetRevision**: Git revision (branch/tag)
- **application.source.path**: path within repo
- **application.source.helm**: Helm options (valueFiles, parameters)
- **application.destination.server/namespace**: deployment target
- **application.syncPolicy**: sync options

## Example

```bash
helm install my-argocd-app ./helm/argocd-app \
  --set application.source.repoURL=https://github.com/example/demo-repo.git \
  --set application.source.targetRevision=main \
  --set application.source.path=helm/nginx \
  --set application.destination.namespace=default
```
