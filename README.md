# Sincronizacion: Exclusión Mutua y Seccion Crítica

## Video Clase 3 - Codigo Fuente

```
raceConditionBank.py
raceConditionBankLock.py
```

## Ejercicio:

```
globalContador.py
```

El siguente programa lanza un conjunto de threads cuyo código es un contador que incrementa una variable global (_contador_) una cierta cantidad de veces. El resultado del programa es la impresión del contenido final de la variable global.

Leer y analizar el código y tratar de deducir que hace cada bloque.

## Preguntas (responder en el campus):

1. Cual es el valor esperado de la variable **_contador_**. En que condiciones se obtendría este valor esperado.
   3000000 es el objetivo esperado y se obtendia en caso de que sea un ejercicio secuencial.

2. Ejecute el programa varias veces y explicar a que se deben los resultados que observa.
   Los resultados se deben a la condicion de carrera, es decir a que los hilos no necesariamente esperan que la funcion finalice y modifique la variable, puede pasar que accedieran a modificar la variable antes de que el anterior hilo la modifique y asi se perdiera el resultado real del contador.

   Los resultados se deben a la condicion de carrera, es decir que los hilos acceden a la seccion critica de la funcion modificando la variable global sin dejar que el anterior hilo termine de utilizar esta misma variable

3. Identifique las Secciones Críticas (incluir las lineas de código en la respuesta).
   global contador
   for i in range(1000000):
    contador += 1

4. Modifique el programa, utilizando Locks de modo que se asegure la exclusión mutua en las secciones críticas.

lock = threading.Lock()

def funcion():
    lock.acquire()
    global contador
    try:
        for i in range(1000000):
            contador += 1
    finally:
            lock.release()

5. Que es una "condición de carrera"? Que consecuencias trae y cuando se produce?

Una condición de carrera es un comportamiento del software en el cual la salida depende del orden de ejecución de eventos que no se encuentran bajo control. Se da cuando uno o mas hilos ejecutan secciones criticas().

6. Que es una Sección Crítica?

La secciona critica es la seccion del codigo donde accediendo a travez de uno o mas hilos se modifica un recurso de la memoria compartida(variable global). 

7. Que es la Exclusión Mútua?

La exclusion mutua trata de asegurar el acceso ordenado a una seccion critica para impedir errores o inconsistencias.

8. Que son los Locks o Mutex? _Bonus (opcional): que es un "deadlock"?, como se produce y que consecuencias tiene?_

Luck o Mutex: es un recurso para armar exclusion mutua en una seccion critica. Antes de entrar en una seccion critica un proceso o thread solicita un lock y el sistema operativo tiene dos opciones:
- si el lock no esta asignado a ningun otro thread o proceso le otorga el permiso par acceder a la seccion critica.
- si el lock esta asignado a otro proceso o thread, el sistema operativo bloquea o duerme a la thread que solicito el lock hasta que este sea liberado.

Deadlock: ocurre cuadno un proceso espera un evento que nunca va a pasar. Se debe dar cuatro condiciones para que se de un deadlock: 
-Los procesos deben reclamar un acceso exclusivo a los recursos.
-Los procesos deben retener los recursos mientras esperan otros.
-Los recursos pueden no ser removidos de los procesos que esperan.
-Existe una cadena circular de procesos donde cada proceso retiene uno o más recursos que el siguiente proceso de la cadena necesita.

<sub>[Daniel Buaon - unahur-progra-concu-1-2021](https://github.com/unahur-progra-concu-1-2021)</sub>
