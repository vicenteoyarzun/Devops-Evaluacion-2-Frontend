# DevOps - Evaluación Parcial N°2 (Innovatech Chile) - Frontend

Este repositorio contiene la interfaz de usuario para el proyecto de **Innovatech Chile**. Se ha diseñado bajo un enfoque de microservicios, asegurando un despliegue optimizado y seguro en la infraestructura de AWS.

## Contenedorización del Frontend

Para este componente se aplicaron las siguientes estrategias de contenedorización:
* **Multi-stage Build:** Se utiliza una etapa de construcción (build) y una etapa de producción ligera para servir el contenido estático.
* **Servidor de Producción:** El contenido se sirve de manera eficiente (usando Nginx o el servidor definido en el Dockerfile).
* **Seguridad:** El contenedor está configurado para ejecutarse con un **usuario con privilegios limitados**, cumpliendo con el estándar de mínimo privilegio.

## Despliegue y CI/CD (GitHub Actions)

El flujo de trabajo automatizado está configurado para activarse con cada `push` en la rama **deploy**:

1. **Construcción y Registro:** El pipeline genera la imagen de Docker del frontend y la sube al registro correspondiente (Docker Hub o ECR).
2. **Despliegue en AWS EC2:** Una vez publicada la imagen, el pipeline se conecta a la instancia de AWS para actualizar el contenedor automáticamente.
3. **Seguridad en el Pipeline:** Se utilizan **GitHub Secrets** para proteger las claves de acceso a AWS y otras variables sensibles.

## Conectividad y Redes

* **Acceso Público:** A diferencia del backend, este contenedor está configurado para ser accesible desde internet a través de la IP pública o dominio de la instancia EC2.
* **Integración:** Se comunica con el contenedor de Backend mediante la red interna definida en Docker Compose, asegurando la integridad de los datos.

## Ejecución Local

1. Clonar el repositorio.
2. Asegurarse de tener configuradas las variables de entorno para apuntar al API del Backend.
3. Ejecutar:
   ```bash
   docker-compose up --build
