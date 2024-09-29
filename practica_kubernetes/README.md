# Implementación de una Aplicación en Kubernetes con MySQL Usando Helm

Este proyecto tiene como finalidad desplegar una aplicación junto con una base de datos MySQL en un clúster de Kubernetes, utilizando Helm como herramienta principal de gestión. Aseguramos la accesibilidad, la escalabilidad y la persistencia de los datos, además de manejar las configuraciones sensibles de manera segura y garantizar la alta disponibilidad (HA) de la aplicación.

## Herramientas Necesarias

Antes de comenzar, asegúrate de tener instaladas las siguientes herramientas:

- **Docker Desktop**: Para ejecutar contenedores localmente.
- **Minikube**: Para crear un clúster local de Kubernetes.
- **Kubectl**: Para gestionar recursos dentro de Kubernetes.
- **Helm**: Para gestionar y desplegar charts en Kubernetes.
- **Visual Studio Code** (o cualquier editor de texto): Para editar archivos YAML y trabajar en el código.
- **MySQL Workbench** (opcional): Para conectarte y gestionar la base de datos MySQL.

## Instalación de Herramientas

1. **Docker Desktop**: Descárgalo desde [Docker Desktop](https://www.docker.com/products/docker-desktop).
2. **Minikube**: 
   ```bash
   brew install minikube

Helm:
brew install helm

Configuración del Clúster
Con las herramientas instaladas, inicia Minikube y configura tu clúster:
minikube start

Estructura del Proyecto
kubernetes_practica/
│
├── Chart.yaml
├── values.yaml
├── templates/
│   ├── deployment.yaml
│   ├── statefulset.yaml
│   ├── service.yaml
│   ├── secrets.yaml
│   ├── ingress.yaml
│   ├── configmap.yaml
│   └── hpa.yaml
└── README.md

Guía Paso a Paso para el Despliegue
Crear el Chart de Helm
Genera un nuevo chart de Helm para tu aplicación:
helm create my-helm-chart
cd my-helm-chart

Configurar Namespaces
Los namespaces permiten organizar tus recursos en Kubernetes. Creamos dos namespaces: uno para la base de datos y otro para la aplicación.
kubectl create namespace db-namespace
kubectl create namespace app-namespace

Configurar Secrets
Crea el archivo secret.yaml y copia el código necesario. Luego aplica el secreto en ambos namespaces:
kubectl apply -f secret.yaml -n db-namespace
kubectl apply -f secret.yaml -n app-namespace

Configurar StatefulSet para la Base de Datos
Aplica el archivo statefulset.yaml en el namespace de la base de datos:
kubectl apply -f statefulset.yaml -n db-namespace

Configurar Deployment para la Aplicación
Despliega tu aplicación usando un Deployment, asegurando escalabilidad y manejabilidad. Aplica el archivo deployment.yaml en el namespace de la aplicación:
kubectl apply -f deployment.yaml -n app-namespace

Configurar Servicios (ClusterIP)
Los servicios permiten la comunicación entre pods y la exposición de la aplicación. Aplica los siguientes archivos:
kubectl apply -f service-db.yaml -n db-namespace
kubectl apply -f service-app.yaml -n app-namespace

Configurar Ingress
Si deseas exponer tu aplicación al exterior del clúster, configura un Ingress aplicando el archivo ingress.yaml:
kubectl apply -f ingress.yaml -n app-namespace

Verificar el Despliegue
Asegúrate de que todos los recursos se hayan desplegado correctamente con los siguientes comandos:
kubectl get all -n db-namespace
kubectl get all -n app-namespace


