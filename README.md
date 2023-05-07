# SREDevOps: discourse-k3s-selfhosted

## WiP: Work in Progress, en desarrollo. Sólo utilizar versiones release, via tags
- k3s: custom configs incluidas en directorio k3s-configs (work in progress)
## Descripción

- Basado en: [Discourse Docker](https://github.com/discourse/discourse_docker)
- ~~Por el momento está estructurado como un proyecto de docker-compose, al tener un stable release se migrará a Kubernetes, testeado en k3s.~~
- Migrado a Kubernetes Deployments y Stateful Sets, testeado en k3s, single node.
- Para los proximos pasos, necesitamos el container de postgres  antes de ejecutar todo el stack, por lo que se debe crear primero el statefulset de postgres para luego crear el deployment de data y web_only.

- La imagen inicial debe crearse con las instrucciones de [Discourse Docker Multiple Containers](https://github.com/discourse/discourse_docker#single-container-vs-multiple-containers), con el "parche" adjunto en este repositorio: [patch-discourse_docker](./patch-discourse-docker/)
- 
- Se utiliza un directorio local para persistir los datos de la base de datos, y otro para persistir los datos de la aplicación.
  - ToDo: Volúmenes persistentes en Kubernetes via NFS 
  - Detalle en cada deployment/statefulset, revisar los puntos de montaje, ejemplo:

```yaml
# deploy/postgres13.yaml
      volumes:
        - name: data
          hostPath:
            path: /root/data-postgres
```

- Crea tus configmap usando el template respectivo con tus valores, ejemplo:

```bash
cp deploy/postgres.env.template deploy/postgres.env
# edita deploy/postgres.env
nano deploy/postgres.env 

# crea el configmap
kubectl create configmap postgres-config --from-file=deploy/postgres.env
```

## Se agradecen pull requests, issues, etc.
