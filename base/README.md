# Base

Common manifests that can be reused as templates.

### FluxCD
First, the kubernetes secret should be setup:
```
kubectl create secret generic flux-git-auth --from-literal=GIT_AUTHUSER=<phab-user> \
  --from-literal=GIT_AUTHKEY=<phab-token> -n flux
```
This will setup `GIT_AUTHUSER` and `GIT_AUTHKEY`.

Then, running `kubectl apply -f install.yaml` will suffice. The (dirty) proxy-related variables will be removed
as soon as Phabricator will be moved inside the WAN.

The `install.yaml` file was generated with the `fluxctl` tool.

The option `--git-path` depends on the environment as well.

The option `--sync-garbage-collection` should in general be set, as it will take care of deleting resources
that are removed from the repository. It does not affect resources that were created without FluxCD.
