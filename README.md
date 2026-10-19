
# Gas Mapocho - API Gateway

Este repositorio contiene el API Gateway del proyecto **Gas Mapocho**, desarrollado para el curso de Desarrollo de Aplicaciones Web II de Cibertec.

El API Gateway funciona como el punto de entrada para las peticiones que llegan al sistema. Su trabajo es recibirlas y dirigirlas al microservicio correspondiente, evitando que los clientes tengan que conectarse directamente a cada servicio.

## Tecnologías utilizadas

- Java 25
- Spring Boot 4.1.1
- Spring Cloud Gateway (Web MVC)
- Netflix Eureka Client
- Spring Cloud Config Client
- Maven
- Docker

## ¿Cómo funciona?

Cuando un cliente realiza una petición, esta llega primero al API Gateway.

Dependiendo de la ruta solicitada, el Gateway se encarga de enviarla al microservicio que debe atenderla.

Por ejemplo, las peticiones relacionadas con pedidos se pueden dirigir al servicio de pedidos, mientras que las relacionadas con pagos se envían al servicio de pagos.

Para esto, el proyecto utiliza Eureka Client, que permite localizar los microservicios registrados en el sistema.

También cuenta con Spring Cloud Config Client para obtener su configuración desde el Config Server.

## Requisitos

Para ejecutar el proyecto necesitamos:

- JDK 25
- Git
- Maven (o utilizar el Maven Wrapper incluido)
- Docker (opcional)
- Eureka Server y Config Server configurados correctamente

## Instalación

Primero clonamos el repositorio:

```bash
git clone https://github.com/Sophia-1827/DAW-II_Grupo09_gasmapocho_api-gateway.git
```

Ingresamos a la carpeta del proyecto:

```bash
cd DAW-II_Grupo09_gasmapocho_api-gateway
```

Compilamos el proyecto:

```bash
.\mvnw.cmd clean install
```

Finalmente, ejecutamos el Gateway:

```bash
.\mvnw.cmd spring-boot:run
```

## Configuración

El Dockerfile del proyecto utiliza el puerto **8080**.

El puerto de ejecución local dependerá de las propiedades configuradas para el servicio.

El API Gateway trabaja junto con dos componentes importantes:

- **Eureka Server:** permite encontrar los microservicios disponibles.
- **Config Server:** proporciona las propiedades de configuración del Gateway.

Las rutas hacia los microservicios se definen mediante la configuración de Spring Cloud Gateway.

## Ejecución con Docker

También podemos ejecutar el proyecto utilizando Docker.

Primero construimos la imagen:

```bash
docker build -t gasmapocho-api-gateway .
```

Luego iniciamos el contenedor:

```bash
docker run -p 8080:8080 gasmapocho-api-gateway
```

Para que funcione correctamente dentro de Docker, debemos asegurarnos de que tenga conexión con Eureka Server, Config Server y los demás servicios necesarios.

## Relación con los demás microservicios

El API Gateway forma parte de la arquitectura de microservicios de Gas Mapocho.

Su función principal es permitir que las peticiones ingresen por un solo punto y sean enviadas al servicio correspondiente.

En nuestro proyecto se relaciona principalmente con:

- **Config Server:** administra las configuraciones del sistema.
- **Eureka Server:** permite el registro y descubrimiento de microservicios.
- **Pedido Service:** se encarga de las operaciones relacionadas con pedidos.
- **Pago Service:** se encarga de las operaciones relacionadas con pagos.

Es recomendable iniciar primero los servicios de infraestructura antes de levantar el API Gateway y los demás microservicios.

## Integrantes

**Grupo 09 - Cibertec**

## Curso

Desarrollo de Aplicaciones Web II
