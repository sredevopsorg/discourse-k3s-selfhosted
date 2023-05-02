# SREDevOps: discourse-k3s-selfhosted

## Descripción

- Basado en: [Libre.sh](https://lab.libreho.st/libre.sh/compose/discourse) y [Discourse](https://github.com/discourse/discourse_docker)
- WiP: Work in Progress, en desarrollo. Sólo utilizar versiones release, via tags.
- Por el momento está estructurado como un proyecto de docker-compose, al tener un stable release se migrará a Kubernetes, testeado en k3s.
- Se utiliza un directorio local para persistir los datos de la base de datos, y otro para persistir los datos de la aplicación.
