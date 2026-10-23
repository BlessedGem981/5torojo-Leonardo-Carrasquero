# 5torojo-Leonardo-Carrasquero
pensamiento computacional
clase 1 modificación de read me

## Parctica1


### 1. Patrón del precio y aumento adicional
Al analizar las diferencias consecutivas del precio total ($10, $18, $24, $28, $30):
* De 1 a 2 arepas: aumenta **$8** ($18 - 10)
* De 2 a 3 arepas: aumenta **$6** ($24 - 18)
* De 3 a 4 arepas: aumenta **$4** ($28 - 24)
* De 4 a 5 arepas: aumenta **$2** ($30 - 28)

> **Patrón:** El incremento por cada arepa adicional no es constante, sino que **disminuye de 2 en 2** a medida que se agregan unidades.

---

### 2. Fórmula matemática ($n$ y $P$)
Dado que el incremento decrece de forma constante, la relación se modela mediante una función cuadrática:

$$P(n) = -n^2 + 11n$$


---

### 3. Predicción del precio para 10 arepas
Sustituyendo $n = 10$ en la fórmula:

$$P(10) = -(10)^2 + 11(10) = -100 + 110 = 10$$

* **Precio predicho para 10 arepas:** **$10** 


---

### 4. Reflexión
* **¿Por qué el precio no aumenta siempre lo mismo?**  
  Representa un esquema comercial de descuento por volumen (economías de escala), donde el costo marginal por unidad disminuye para incentivar la compra de mayor cantidad.
* **¿Qué pasaría si el patrón cambiara?**  
  * Si el patrón fuera lineal, el precio aumentaría a un costo constante por unidad sin ofrecer incentivos al comprador.
  * Además, el comportamiento matemático del modelo cuadrático muestra que después de cierto punto los valores decrecen, lo que evidencia que las fórmulas matemáticas tienen un rango de validez práctico en el mundo real.

---
## Practica2

[Tinkercad circuito](https://www.tinkercad.com/things/7oEBFdjXngn-practica-3-led?sharecode=ls7F3lmKjk6TOtskgJKShXZA7ilyjbBxP4iNFuZ4Qg8)

[Imagen de la actividad](./imagenes/actividad2.png)

## Practica 3


## Practica 4





### Centro de Atencion para Estudiantes

#### 1. Descomposicion en subproblemas

* **Llegada y registro:** Capturar los datos iniciales del estudiante (identificacion, tipo de tramite y si presenta alguna condicion de prioridad).
* **Gestion de prioridades y colas:** Organizar a los estudiantes en estructuras de datos adecuadas (cola regular para atencion en orden de llegada y cola prioritaria para casos especiales).
* **Atencion en ventanilla:** Asignar el turno libre al siguiente estudiante siguiendo la jerarquia de colas y realizar el tramite correspondiente.
* **Cierre y estadisticas:** Finalizar la atencion registrando metricas de desempeno (tiempos de espera, cantidad de personas atendidas y reportes diarios).

#### 2. Datos necesarios para representar a cada estudiante

* `id_estudiante` (Texto o entero: Numero de identificacion o carnet).
* `tipo_tramite` (Entero/Texto: 1 = Entrega de documentos, 2 = Solicitud de constancia, 3 = Consulta general).
* `hora_llegada` (Marca de tiempo: Hora exacta de ingreso al centro para mantener el orden FIFO).
* `es_prioritario` (Booleano: Verdadero / Falso segun condiciones especiales como movilidad reducida o emergencias).
* `tiempo_estimado` (Entero: Minutos aproximados de duracion segun el tipo de tramite).

#### 3. Algoritmo en pseudocodigo

```text
Inicio
    Definir cola_regular como Cola vacia
    Definir cola_prioritaria como Cola vacia
    
    Mientras el centro de este abierto Hacer
        Si llega_estudiante() Entonces
            Leer datos (id_estudiante, tipo_tramite, es_prioritario)
            Si es_prioritario == Verdadero Entonces
                Agregar_a_cola(cola_prioritaria, estudiante)
            Sino
                Agregar_a_cola(cola_regular, estudiante)
            FinSi
        FinSi
        
        Si ventanilla_disponible() Y (no_vacia(cola_prioritaria) O no_vacia(cola_regular)) Entonces
            Si no_vacia(cola_prioritaria) Entonces
                estudiante_actual = extraer(cola_prioritaria)
            Sino
                estudiante_actual = extraer(cola_regular)
            FinSi
            Atender(estudiante_actual)
        FinSi
    FinMientras
    
    Mostrar reporte_del_dia()
Fin

```

#### 4. Criterio de prioridad elegido y justificacion

* **Criterio:** Atencion mixta (Atencion preferencial para casos de prioridad + Orden FIFO estricto para el resto).
* **Justificacion:** Mantiene la equidad y el respeto por el orden de llegada de la mayoria de los estudiantes, garantizando a su vez una respuesta rapida ante emergencias o necesidades especiales sin saturar la ventanilla unica.

---

### Ruta del Autobus Escolar

#### 1. Representacion de paradas y distancias

Se representan 6 paradas (P1 a P6) y la Escuela (E) mediante la siguiente tabla de distancias y carga de estudiantes:

| Parada | Estudiantes | Conexiones y distancias (km) |
| --- | --- | --- |
| **Parada 1 (P1)** | 4 | P1 hacia P2 (2 km), P1 hacia P3 (5 km) |
| **Parada 2 (P2)** | 6 | P2 hacia P3 (3 km), P2 hacia P5 (6 km) |
| **Parada 3 (P3)** | 3 | P3 hacia P4 (2 km), P3 hacia P6 (7 km) |
| **Parada 4 (P4)** | 5 | P4 hacia P5 (4 km), P4 hacia P6 (3 km) |
| **Parada 5 (P5)** | 2 | P5 hacia P6 (2 km), P5 hacia Escuela (5 km) |
| **Parada 6 (P6)** | 4 | P6 hacia Escuela (3 km) |

#### 2. Algoritmo paso a paso para construir la ruta

1. **Inicio:** Salir desde la ubicacion inicial hacia la primera parada con estudiantes.
2. **Evaluacion:** Desde la posicion actual, evaluar la distancia hacia todas las paradas pendientes por visitar.
3. **Seleccion:** Elegir la parada no visitada que represente la menor distancia recorrida (Estrategia del vecino mas cercano).
4. **Recoleccion:** Avanzar a la parada seleccionada, embarcar a los estudiantes y marcar la parada como completada.
5. **Cierre:** Repetir los pasos 2 a 4 hasta completar las 6 paradas y finalizar el trayecto en la Escuela.

#### 3. Aplicacion del algoritmo y ruta propuesta

* **Secuencia de la ruta:** P1 -> P2 -> P3 -> P4 -> P5 -> P6 -> Escuela
* **Total de estudiantes recogidos:** 4 + 6 + 3 + 5 + 2 + 4 = 24 estudiantes
* **Distancia total recorrida:** 2 + 2 + 3 + 2 + 4 + 2 + 3 = 18 km

#### 4. Comparacion con ruta alternativa

* **Ruta Alternativa B:** P6 -> P5 -> P4 -> P3 -> P2 -> P1 -> Escuela
* **Distancia total de la Alternativa B:** 21 km
* **Conclusion:** La Ruta Propuesta es optima bajo el criterio de menor distancia recorrida (18 km frente a 21 km), reduciendo el consumo de combustible y el tiempo total en transito.

---

### Correccion de Pseudocodigo (Promedio de Notas)

#### 1. Errores o limitaciones identificados

* **Error matematico en el calculo:** El codigo original realizaba la suma de las notas (nota1 + nota2 + nota3), pero no dividia el resultado entre 3, almacenando la suma total en lugar del promedio.
* **Ausencia de validacion de entradas:** No verificado si los valores ingresados se encontraban en un rango de notas valido (por ejemplo, entre 0 y 100).
* **Falta de salida informativa:** No mostraba al usuario el valor numerico obtenido en la variable promedio.

#### 2 y 3. Pseudocodigo corregido con validacion (0 a 100)

```text
Inicio
    Escribir "Ingrese la nota 1 (0 a 100):"
    Leer nota1
    Escribir "Ingrese la nota 2 (0 a 100):"
    Leer nota2
    Escribir "Ingrese la nota 3 (0 a 100):"
    Leer nota3
    
    Si (nota1 >= 0 Y nota1 <= 100) Y (nota2 >= 0 Y nota2 <= 100) Y (nota3 >= 0 Y nota3 <= 100) Entonces
        
        promedio = (nota1 + nota2 + nota3) / 3
        
        Escribir "El promedio obtenido es: ", promedio
        
        Si promedio >= 60 Entonces
            Escribir "Estado: Aprueba"
        SiNo
            Escribir "Estado: No aprueba"
        FinSi
        
    SiNo
        Escribir "Error: Una o mas notas ingresadas estan fuera del rango permitido (0 a 100)."
    FinSi
Fin

```

#### 4. Mejora adicional propuesta

Se incorpora un estado intermedio de recuperacion para estudiantes con promedio entre 50 y 59 puntos:

```text
Si promedio >= 60 Entonces
    Escribir "Estado: Aprueba"
SinoSi promedio >= 50 Y promedio < 60 Entonces
    Escribir "Estado: Requiere prueba de recuperacion"
SiNo
    Escribir "Estado: No aprueba"
FinSi

```

