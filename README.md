# Evaluación Parcial N°2 – DevOps, Docker y CI/CD

## Integrantes

* Juan Vargas
* Matilda Vargas

## Descripción del proyecto

Este proyecto corresponde a la Evaluación Parcial N°2 de la asignatura DevOps.

La solución está compuesta por:

* Microservicio de Ventas (Spring Boot)
* Microservicio de Despachos (Spring Boot)
* Frontend (React + Vite)
* Base de Datos MySQL

La aplicación fue contenedorizada utilizando Docker y Docker Compose, permitiendo su ejecución en entornos locales y servidores Linux.

Además, se implementó un pipeline CI/CD mediante GitHub Actions para automatizar la construcción y publicación de imágenes Docker en Docker Hub.

---

# Arquitectura

Frontend (React)
↓
Microservicio Ventas (Spring Boot)
↓
MySQL

Frontend (React)
↓
Microservicio Despachos (Spring Boot)
↓
MySQL

Todos los servicios se ejecutan mediante contenedores Docker conectados en una misma red creada por Docker Compose.

---

# Tecnologías utilizadas

* Java 17
* Spring Boot 3
* Maven
* React
* Vite
* MySQL 8
* Docker
* Docker Compose
* GitHub Actions
* Docker Hub

---

# Estructura del proyecto

```text
evaluacion2-devops/
│
├── back-Ventas_SpringBoot/
│
├── back-Despachos_SpringBoot/
│
├── front_despacho/
│
├── docker-compose.yml
│
└── .github/
    └── workflows/
        └── deploy.yml
```

# Dockerfiles

Cada componente posee su propio Dockerfile.

Se utilizó Multi-Stage Build para los microservicios Spring Boot:

1. Etapa Builder:

   * Compilación con Maven Wrapper.
   * Generación del archivo JAR.

2. Etapa Runtime:

   * Imagen liviana Eclipse Temurin JRE.
   * Ejecución de la aplicación compilada.

Beneficios:

* Menor tamaño de imagen.
* Mejor rendimiento.
* Separación entre compilación y ejecución.

---

# Persistencia de datos

La base de datos utiliza un volumen Docker nombrado:

```yaml
volumes:
  mysql_data:
```

Este volumen almacena la información de MySQL fuera del ciclo de vida del contenedor.

Ventajas:

* Los datos no se pierden al reiniciar contenedores.
* Permite actualizaciones sin afectar la información almacenada.

Se eligió un Named Volume por simplicidad, portabilidad y facilidad de administración.

---

# Configuración Docker Compose

Para levantar todos los servicios:

```bash
docker compose up -d
```

Para detenerlos:

```bash
docker compose down
```

Servicios incluidos:

* mysql
* ventas
* despachos
* frontend

---

# Variables de entorno

Los microservicios utilizan variables de entorno para conectarse a MySQL.

Ejemplo:

```yaml
environment:
  DB_ENDPOINT: mysql
  DB_PORT: 3306
  DB_NAME: despacho_db
  DB_USERNAME: root
  DB_PASSWORD: root
```

La URL de conexión fue parametrizada mediante:

```properties
spring.datasource.url=jdbc:mysql://${DB_ENDPOINT}:${DB_PORT}/${DB_NAME}?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC&createDatabaseIfNotExist=true
```

Esto permite reutilizar la misma aplicación en distintos entornos.

---

# CI/CD con GitHub Actions

Se implementó un workflow llamado:

```text
.github/workflows/deploy.yml
```

El pipeline se ejecuta automáticamente al realizar push sobre la rama:

```text
deploy
```

Etapas:

1. Checkout del repositorio.
2. Login en Docker Hub.
3. Build imagen ventas.
4. Push imagen ventas.
5. Build imagen despachos.
6. Push imagen despachos.
7. Build imagen frontend.
8. Push imagen frontend.

---

# Imágenes publicadas

Docker Hub:

```text
jvc1610/ventas-service:latest
jvc1610/despachos-service:latest
jvc1610/front-despacho:latest
```

---

# Ejecución mediante imágenes publicadas

Descargar imágenes:

```bash
docker compose pull
```

Levantar servicios:

```bash
docker compose up -d
```

Verificar contenedores:

```bash
docker ps
```

---

# Verificación de funcionamiento

Backend Ventas:

```bash
curl http://localhost:8086/api/v1/ventas
```

Backend Despachos:

```bash
curl http://localhost:8087/api/v1/despachos
```

Frontend:

```bash
curl http://localhost:3018
```

---

# Seguridad

Se utilizaron GitHub Secrets para almacenar credenciales sensibles:

* DOCKER_USERNAME
* DOCKER_TOKEN

Las credenciales no se almacenan dentro del código fuente.

---

# Principios DevOps aplicados

* Contenedorización con Docker.
* Persistencia mediante volúmenes.
* Automatización CI/CD.
* Control de versiones con Git.
* Integración continua.
* Entrega continua.
* Infraestructura reproducible.
* Separación por microservicios.

---

# Conclusión

La solución permite construir, publicar y desplegar automáticamente los componentes del sistema mediante Docker y GitHub Actions.

El uso de contenedores facilita la portabilidad, mientras que la automatización reduce errores manuales y mejora la velocidad de despliegue.
