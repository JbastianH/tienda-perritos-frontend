# Tienda de Perritos - Frontend

## Descripción del Proyecto
El presente repositorio expone la interfaz de usuario (Frontend) para el proyecto "Tienda de Perritos". La aplicación web consume los servicios expuestos por el backend y es accesible al usuario final mediante una URL pública.

## Arquitectura y Tecnologías
La aplicación se despliega en un entorno de contenedores gestionado por **Amazon EKS**.
* **Registro de Contenedores:** Amazon ECR.
* **Redes:** Se expone la aplicación hacia internet a través de un servicio tipo `LoadBalancer` asociado a las subredes públicas de la VPC en AWS.
* **Escalabilidad:** Se utiliza Horizontal Pod Autoscaler (HPA) para gestionar la demanda de tráfico.

## Flujo de Integración y Despliegue Continuo (CI/CD)
Se automatiza la entrega continua utilizando **GitHub Actions**. El pipeline configurado realiza las siguientes tareas:
1. Se conecta con las credenciales de AWS.
2. Se compila la imagen Docker del frontend.
3. Se envía la imagen empaquetada al repositorio de Amazon ECR.
4. Se despliegan los cambios en el clúster EKS, asegurando la actualización sin interrupción del servicio gracias a los ReplicaSets de Kubernetes.

## Estructura del Repositorio
* `/`: Código fuente de la interfaz web web y archivo `Dockerfile`.
* `/k8s`: Manifiestos YAML correspondientes a la orquestación del frontend (`Deployment`, `Service`, `HPA`).

## Instrucciones de Configuración
Para el correcto funcionamiento del pipeline de despliegue, se deben registrar las credenciales de conexión en los secretos del repositorio:
* `AWS_ACCESS_KEY_ID`
* `AWS_SECRET_ACCESS_KEY`
* `AWS_SESSION_TOKEN`