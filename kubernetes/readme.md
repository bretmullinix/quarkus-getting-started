# Tekton Artifacts

## Purpose

Get use to Tekton.  

## Good References

https://github.com/brightzheng100/tekton-pipeline-example

Apply the buildah task locally in namespace:  kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/buildah/0.4/buildah.yaml

## SA Secrets

1. Make sure you create your github_token.yaml and reference it in your SA definition
1. Make sure you create all your container registry secrets and reference them in your SA definition

    ```
    kubectl create secret -n test-quarkus docker-registry <registry name goes here>-registry-secret \
     --docker-server=$CONTAINER_REGISTRY_SERVER \
     --docker-username=$CONTAINER_REGISTRY_USER \
      --docker-password=$CONTAINER_REGISTRY_PASSWORD
    ```

1. Add escalated privs for to run the pipeline

    ```
    oc adm policy add-scc-to-user anyuid -z pipeline-sa -n test-quarkus
    ```

1. Add privileged to SA run pipeline

    ```
    oc adm policy add-scc-to-user privileged -z pipeline-sa -n test-quarkus
    ```