# Mutant Analyzer – UTN

Proyecto desarrollado en **Spring Boot** para el análisis de secuencias de ADN, con el objetivo de determinar si corresponden a un mutante. La solución integra lógica de detección, API REST y persistencia con estadísticas, cumpliendo con los tres niveles establecidos en la consigna.

## Tecnologías utilizadas

* **Java 17**
* **Spring Boot** (Web, Data JPA, Validation)
* **H2 Database** para persistencia en memoria
* **Gradle** como gestor de dependencias
* **JUnit y Mockito** para pruebas automáticas
* **Lombok** para reducir boilerplate
* **Spring Boot Starter Test** para testing de integración

## Dependencias principales (build.gradle)

El proyecto utiliza, entre otras, las siguientes librerías:

* `spring-boot-starter-web`: estructura de API REST.
* `spring-boot-starter-data-jpa`: acceso y mapeo a base de datos.
* `com.h2database:h2`: motor de base de datos en memoria.
* `lombok`: generación automática de getters, setters y constructores.
* `spring-boot-starter-test`: herramientas de testing.

## Nivel 1 – Lógica de detección

Se implementa un algoritmo que analiza una matriz de ADN (NxN) y determina si existen más de una secuencia de cuatro caracteres iguales consecutivos en sentido horizontal, vertical o diagonal. El método retorna un valor booleano que clasifica la secuencia como mutante o humana.

## Nivel 2 – API REST

Se expone un servicio HTTP que recibe la secuencia de ADN en formato JSON.

### POST /mutant/analizar

Solicitud:

```json
{
  "dna": ["ATGCGA","CAGTGC","TTATGT","AGAAGG","CCCCTA","TCACTG"]
}
```

Respuestas:

* **200 OK:** mutante
* **403 Forbidden:** humano

El proyecto está preparado para despliegue en plataformas cloud gratuitas como Render.

## Nivel 3 – Persistencia y estadísticas

Se integra una base de datos **H2** para registrar cada secuencia analizada, asegurando un único registro por ADN.
Se incorpora el endpoint:

### GET /stats

Retorna la cantidad de ADN mutante, humano y el ratio entre ambos valores.

## Diagrama de secuencia

El repositorio incluye el diagrama de secuencia correspondiente al flujo completo del endpoint `/mutant/analizar`.

```
sequence-diagram.png
```

## Ejecución

1. Clonar el repositorio:

```bash
git clone https://github.com/TomCab98/utn-mutant-analyzer.git
```

2. Ejecutar la aplicación:

```bash
./gradlew bootRun
```

3. Acceso opcional a H2:

```
http://localhost:8080/h2-console
```
