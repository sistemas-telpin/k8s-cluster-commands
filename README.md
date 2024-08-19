# k8s-cluster-commands

[![Preview](https://telpin.com.ar/wp-content/uploads/2023/02/logo-telpin-180x66-1.png)](https://telpin.com.ar)

Github Action para interactuar con un cluster de K8s provisto por Telpin. Prepara un entorno seguro para ejecutar comandos kubectl ([k8s](https://kubernetes.io)).

## Secretos a configurar

Para utilizar la acción, es necesario definir dos _secrets_ a nivel de repositorio:

- KUBE_CONFIG
- V2RAY_CONFIG

Estos secrets deben estar expresados en BASE64, y se deben usar los siguientes comandos para obtenerlos.

Dado el archivo **cluster-credentials.yml** provisto por Telpin:

```console
base64 cluster-credentials.yml | tr -d '\n' | tee
```

y dado el archivo de configuración de V2RAY provisto por Telpin:

```console
base64 config.json | tr -d '\n' | tee
```

## Forma de uso

Para ejecutar comandos **kubectl** en un workflow:

```yaml
- uses: sistemas-telpin/k8s-cluster-commands@1.0.9
  with:
    KUBE_CONFIG: ${{ secrets.KUBE_CONFIG }}
    V2RAY_CONFIG: ${{ secrets.V2RAY_CONFIG }}
    commands: |
      kubectl -n SAMPLENS rollout restart deployment deployment-1
      kubectl -n SAMPLENS apply -f /config.yml
      kubectl get pods
```
