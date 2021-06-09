# Sentry con Helm

## Precondiciones:

### 1- Crear PostgreSQL en AWS RDS:

ej.
- Username: sentry
- Database: sentry
- Password: sentrysentry
- Port: 5432
- type: t3.small
- Security Groups:

### 2- Crear Redis en AWS ElasticCache:

ej.
- Port: 6379
- Node Type: cache.t3.small
- Replicas: 0 (si ponés 1, crea la original máś una replica, en conclusión te crea 2 nodos, y eso no queremos)
- Multi-AZ: disable
- Security Groups:

## Crear Namespace en Cluster Kubernetes:

### 3- Creamos un nuevo namespace llamado sentry:

``` kubectl create namespace sentry ```

## Helm

### 4- Agregamos el repo de sentry:

- ``` helm repo add sentry https://sentry-kubernetes.github.io/charts ``` (deprecado)
- ``` helm repo add stable https://charts.helm.sh/stable ```

### 5- Listamos los repos:

``` helm repo list ```
                                       
- sentry	https://sentry-kubernetes.github.io/charts
- stable	https://charts.helm.sh/stable

### 6- Instalamos el chart de Helm de Sentry usando el archivo values.yaml:

``` helm install --wait -f values.yaml sentry --namespace sentry stable/sentry ```

- -f values.yaml : es el archivo que contiene todas las config
- "sentry" : es el nombre que tendrá el deploy
- --namespace sentry : en que namespace se deployará
- stable/sentry : es el repo del helm

### Opciones:

#### Para eliminar el deploy creado:

``` helm delete sentry --namespace sentry```

#### Ver info sobre el Helm creado:

``` helm get all sentry```

### Source:

- https://hub.kubeapps.com/charts/stable/sentry
- https://github.com/helm/charts/tree/master/stable/sentry
- https://github.com/sentry-kubernetes/charts
- https://hub.kubeapps.com/charts/stable/sentry/0.1.3

- https://www.youtube.com/watch?v=e4wiWkz0iYU

- https://helm.sh/docs/intro/using_helm/
