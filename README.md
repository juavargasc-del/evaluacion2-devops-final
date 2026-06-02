# 📦 Innovatech Chile - Sistema de Microservicios con Docker y CI/CD

## Descripción

Este proyecto corresponde a la implementación de una solución basada en microservicios para la empresa Innovatech Chile.

La aplicación está compuesta por un frontend web, dos microservicios backend (Ventas y Despachos) y una base de datos MySQL. La infraestructura fue contenedorizada utilizando Docker y orquestada mediante Docker Compose, permitiendo una ejecución consistente y portable en distintos entornos.

Además, se implementó un pipeline de Integración Continua (CI) mediante GitHub Actions para automatizar la construcción y publicación de imágenes Docker.

---

## Repositorio

Repositorio oficial del proyecto:

https://github.com/juavargasc-del/evaluacion2-devops-final.git

---

## Arquitectura de la Solución

La arquitectura está compuesta por los siguientes componentes:

* Frontend Web
* Microservicio de Ventas
* Microservicio de Despachos
* Base de Datos MySQL

Cada componente se ejecuta dentro de su propio contenedor Docker, manteniendo independencia entre servicios y facilitando la escalabilidad y mantenibilidad de la solución.

---

## Tecnologías Utilizadas

* Java 17
* Spring Boot
* React
* Docker
* Docker Compose
* MySQL 8
* Git
* GitHub
* GitHub Actions
* Docker Hub

---

## Estructura General del Proyecto

El repositorio se encuentra organizado en módulos independientes para cada componente del sistema:

* Frontend
* Backend Ventas
* Backend Despachos
* Configuración Docker Compose
* Pipeline CI/CD

Esta estructura permite mantener una separación clara de responsabilidades entre los distintos servicios.

---

## Contenedorización

Todos los componentes fueron preparados para ejecutarse dentro de contenedores Docker.

La solución incorpora:

* Imágenes independientes por servicio.
* Configuración de puertos y dependencias.
* Variables de entorno para configuración flexible.
* Construcción optimizada de imágenes.
* Ejecución integrada mediante Docker Compose.

---

## Persistencia de Datos

La persistencia se implementó utilizando volúmenes Docker administrados por la plataforma.

Esta configuración permite conservar la información almacenada en la base de datos incluso ante reinicios o recreación de contenedores, asegurando la continuidad operativa del sistema.

---

## Integración Continua (CI)

Se implementó un flujo automatizado mediante GitHub Actions.

Cada actualización enviada a la rama de despliegue genera automáticamente:

* Obtención del código fuente.
* Construcción de imágenes Docker.
* Publicación de imágenes en Docker Hub.

Esta automatización reduce errores manuales y asegura la trazabilidad de los cambios realizados durante el desarrollo.

---

## Gestión Segura de Credenciales

Las credenciales utilizadas durante el proceso de construcción y publicación de imágenes son gestionadas mediante GitHub Secrets.

Esto permite proteger información sensible y seguir buenas prácticas de seguridad dentro del flujo DevOps.

---

## Ejecución del Proyecto

La aplicación puede ser desplegada utilizando Docker Compose, permitiendo levantar toda la arquitectura de servicios de forma centralizada.

Una vez iniciados los contenedores, los distintos componentes quedan disponibles según la configuración definida para cada servicio.

---

## Acceso a la Aplicación

Frontend desplegado:

http://190.46.216.53:3018/

---

## Buenas Prácticas Implementadas

Durante el desarrollo se aplicaron principios y prácticas DevOps orientadas a la mantenibilidad y automatización:

* Arquitectura basada en microservicios.
* Contenedorización mediante Docker.
* Orquestación con Docker Compose.
* Persistencia de datos mediante volúmenes.
* Automatización de procesos con GitHub Actions.
* Gestión segura de credenciales.
* Control de versiones con Git y GitHub.

---

## Evidencias Consideradas

La documentación complementaria de la evaluación incluye evidencia de:

* Construcción de imágenes Docker.
* Publicación de imágenes en Docker Hub.
* Ejecución de contenedores.
* Funcionamiento de GitHub Actions.
* Persistencia de datos.
* Funcionamiento de la aplicación desplegada.

---

## Conclusión

La solución desarrollada cumple con los requerimientos de contenedorización, persistencia y automatización solicitados para la evaluación.

La arquitectura implementada proporciona una base sólida para futuras mejoras, permitiendo ejecutar la aplicación de forma consistente, mantener la separación entre servicios y facilitar los procesos de integración continua dentro de un entorno DevOps.
