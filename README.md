# Mutant Analyzer – UTN

El presente proyecto implementa un sistema de análisis de secuencias de ADN utilizando Spring Boot, con el objetivo de determinar si un individuo corresponde a un mutante según los criterios establecidos en la consigna. La solución aborda de manera completa los tres niveles requeridos: lógica de detección, exposición mediante API REST y persistencia con generación de estadísticas.

## Nivel 1 – Lógica de detección

Se desarrolla un algoritmo que evalúa matrices de ADN de tamaño NxN, identificando la presencia de más de una secuencia de cuatro caracteres idénticos consecutivos en dirección horizontal, vertical o diagonal.
El método retorna un valor booleano que indica si la secuencia corresponde a un mutante.

## Nivel 2 – API REST

Se expone un servicio REST destinado a recibir secuencias de ADN y determinar su clasificación.

### Endpoint: POST /mutant/analizar

**Ejemplo de solicitud:**

```json
{
  "dna": ["ATGCGA","CAGTGC","TTATGT","AGAAGG","CCCCTA","TCACTG"]
}
```

**Respuestas esperadas:**

* **200 OK**: El ADN corresponde a un mutante.
* **403 Forbidden**: El ADN pertenece a un humano.

La aplicación está preparada para su despliegue en plataformas cloud gratuitas como Render.

## Nivel 3 – Persistencia y estadísticas

Se incorpora una base de datos H2 para registrar cada secuencia analizada, garantizando un único registro por ADN. Se almacena la condición (mutante/humano) resultante del análisis.

### Endpoint: GET /stats

**Ejemplo de respuesta:**

```json
{
  "count_mutant_dna": 40,
  "count_human_dna": 100,
  "ratio": 0.4
}
```

El proyecto incluye pruebas automáticas y una cobertura superior al 80%. Asimismo, se presenta el diagrama de secuencia correspondiente al flujo de procesamiento:

### Diagrama de secuencia

<img width="815" height="741" alt="diag de secuencia" src="https://github.com/user-attachments/assets/80b5bd6b-dbf5-4a9c-834d-5ba7c2459884" />

## Ejecución

### 1. Clonar el repositorio

```bash
git clone https://github.com/TomCab98/utn-mutant-analyzer.git
```

### 2. Ejecutar la aplicación

```bash
./gradlew bootRun
```

### 3. Acceso a la consola H2 (opcional)

```
http://localhost:8080/h2-console
```

---

Si deseás, puedo generar también una versión aún más técnica, o un formato estilo informe académico.
