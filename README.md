# Kubernetes helm charts for xinference

## Usage
```
# add repo
helm repo add xinference https://xorbitsai.github.io/xinference-helm-charts

# update indexes and query xinference versions
helm repo update
helm search repo xinference/xinference --devel --versions

# install xinference
helm install xinference xinference/xinference -n xinference --version 0.0.1-v<xinference_release_version>
```

## Custom Install
By default, the installation is similar to a local single-machine deployment of Xinference, 
meaning there is only one worker, and all other parameters remain at their default settings.

Below are some common custom installation configurations.

1. I need to download models from `ModelScope`.
    ```
    helm install xinference xinference/xinference -n xinference --version 0.0.1-v<xinference_release_version> --set config.model_src="modelscope"
    ```
2. I want to use cpu image of xinference (or use any version of xinference images).
    ```
    helm install xinference xinference/xinference -n xinference --version 0.0.1-v<xinference_release_version> --set config.xinference_image="<xinference_docker_image>"
    ```
3. I want to have 4 Xinference workers, with each worker managing 4 GPUs.
    ```
    helm install xinference xinference/xinference -n xinference --version 0.0.1-v<xinference_release_version> --set config.worker_num=4 --set config.gpu_per_worker="4"
    ```

The above installation is based on the `--set` option of `Helm`. 
For more complex custom installations, such as configuring shared storage between workers, it is recommended to provide your own `values.yaml` file using the `-f` option. 
The default `values.yaml` is located at `charts/xinference/values.yaml`. 
For some examples, please refer to `examples/`.
