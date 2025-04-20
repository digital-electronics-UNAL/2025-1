# Comparación entre tecnología CMOS y TTL

## Contenido

1. [Introducción](#1-introducción)
2. [Objetivos](#2-objetivos)
3. [Trabajo previo](#3-trabajo-previo)
4. [Recursos requeridos](#4-recursos-requeridos)
5. [Procedimiento](#5-procedimiento)
6. [Entregables](#6-entregables)
7. [Referencias](#7-referencias)
8. [Material de apoyo](#8-material-de-apoyo)


## 1. Introducción
En el diseño de sistemas digitales, es fundamental comprender las características eléctricas de las distintas familias lógicas, ya que estas determinan el rendimiento, consumo de energía, compatibilidad y robustez del circuito. Dos de las familias más utilizadas son TTL (Transistor-Transistor Logic) y CMOS (Complementary Metal-Oxide Semiconductor), cada una con ventajas y limitaciones particulares **[1]**.

Las compuertas TTL, basadas en transistores bipolares, ofrecen alta velocidad de conmutación y una arquitectura robusta, pero presentan un consumo estático considerable y son susceptibles a picos de corriente en las transiciones. Durante la conmutación, los transistores bipolares atraviesan regiones de operación que provocan ráfagas momentáneas de corriente desde la fuente de alimentación, lo cual puede introducir ruido en el sistema si no se aplican técnicas de desacoplo apropiadas (como el uso de capacitores de bypass) **[1]**.

Por su parte, las compuertas CMOS, construidas con transistores MOS complementarios, presentan un consumo estático prácticamente nulo y una alta inmunidad al ruido, lo que las hace ideales para dispositivos portátiles o entornos industriales. Aunque también experimentan picos de corriente breves durante la conmutación, su magnitud es mucho menor que en TTL, gracias a la alta impedancia de entrada y la baja corriente de operación típica de los transistores MOS. Aun así, el uso de capacitores de desacoplo sigue siendo recomendable para evitar fluctuaciones en la alimentación durante transiciones rápidas **[1]**.

En esta práctica se realizará un análisis comparativo entre dispositivos TTL y CMOS mediante la implementación de una operación lógica elemental. Se evaluarán sus características eléctricas, tiempos de respuesta, curvas de transferencia y comportamiento dinámico, tanto mediante simulación como a través de mediciones experimentales, con el objetivo de comprender las implicaciones prácticas de cada tecnología en el diseño digital


## 2. Objetivos

* Comparar el comportamiento eléctrico de compuertas lógicas fabricadas en tecnologías TTL y CMOS.

* Evaluar la respuesta temporal, disipación de potencia y niveles lógicos de dispositivos digitales.


## 3. Trabajo previo

Antes de realizar la actividad en laboratorio, se deberá llevar a cabo una simulación preliminar utilizando modelos SPICE de los dispositivos a analizar. Este trabajo incluye:

1. **Comparación de especificaciones técnicas**:

   *  Obtener y analizar las hojas de datos (datasheets) de los dispositivos 74LS04 (TTL) y CD4069 (CMOS). Comparar los parámetros clave de cada tecnología como $V_{IH}​$, $V_{IL}​$, $V_{OH}$, $V_{OL}$, tiempos de subida, bajada, y retardo de propagación, entre otros.

2. **Circuito equivalente**:

   * Determinar y dibujar el circuito equivalente para cada uno de los dispositivos basándose en lo visto en la clase magistral.

3. **Importación y configuración de modelos SPICE**:

   * Importar y configurar correctamente los modelos SPICE del 74LS04 (TTL) y el CD4069 (CMOS) en el simulador. Se recomienda revisar la sección [Material de apoyo](#8-material-de-apoyo).


4. **Simulación de comportamiento ante señales de entrada**:

   * Realizar la simulación de cada compuerta lógica ante señales de entrada de diferentes frecuencias (desde 100 Hz hasta 1 MHz).

   * Observar cómo la frecuencia de entrada afecta la respuesta temporal y la disipación de potencia.

5. **Función de transferencia $V_{in}$ vs $V_{out}$​**:

   * Obtener la función de transferencia para cada compuerta (TTL y CMOS).

   * A partir de esta curva, determinar $V_{IH}​$, $V_{IL}​$, $V_{OH}$, $V_{OL}$.

6. **Estimación de tiempos de conmutación**:

   * Obtenier tiempos de subida ($t_r$), bajada ($t_f$) y retardo ($t_{PLH}$, $t_{PHL}$ y $t_{P}$) para cada tecnología.

7. **Estimación del consumo de potencia**:

   * Estimar teóricamente y en simulación la potencia estática y la potencia dinámica de cada dispositivo durante la operación.

   * Analizar cómo varía el consumo de potencia en función de la frecuencia de operación y el tipo de tecnología (TTL vs CMOS), considerando las características de cada tecnología.

8. **Simulación de oscilador en anillo**:

   * Estudiar el oscilador en anillo basado en la compuerta NOT.

   <div align="center">
   <img src="/pics/lab01/osc.png" alt="ring-osc" style="width: 600px; height: auto;">
   </div>


   * Simular el comportamiento de los osciladores en anillo utilizando compuertas NOT CMOS, solicitados en la [parte 3](#parte-3).

9. Realizar la investigación teórica que se considere relevante según los aspectos solicitados en la práctica, como las características eléctricas, niveles lógicos, tiempos de conmutación y consumo de potencia de las tecnologías TTL y CMOS

Este trabajo servirá como base de comparación para los resultados obtenidos en el laboratorio.

## 4. Recursos requeridos

* Compuerta NOT TTL: 74LS04
* Compuerta NOT CMOS: CD4069
* Simulador de circuitos (LTSpice u otro compatible con modelos SPICE)
* Modelos SPICE de los dispositivos
* Hojas de datos (datasheets) de los dispositivos
* Fuente de alimentación 
* Generador de funciones y osciloscopio con puerto USB
* USB

## 5. Procedimiento

### Parte 1

1. Aplicar una señal triangular de 1 kHz de tensión adecuada para obtener la función de transferencia $V_{out}$ vs $V_{in}$ y a partir de la función de transferencia determinar experimentalmente los parámetros  $V_{IH}$, $V_{IL}$, $V_{OH}$, $V_{OL}$.
2. Medir experimentalmente el tiempo de subida ($t_r$), tiempo de bajada ($t_f$), tiempo de retardo ($t_{PHL}$ y $t_{PLH}$) para cada dispositivo.

### Parte 2

1. Determinar el fan-in y fan-out de cada uno de los dispositivos.

2. Determinar el consumo de potencia de cada dispositivo.

3. Proponer e implementar un circuito de entrada y de salida para cada uno de los dispositivos teniendo en cuenta los parámetros de cada tecnología para observar el comportamiento del mismo.

### Parte 3

1. Implementar dos configuraciones diferentes de osciladores en anillo utilizando compuertas CMOS. Observar y registrar la frecuencia de oscilación generada por cada configuración.

2. Comparar el desempeño de las dos configuraciones de osciladores en anillo, analizando las diferencias en la forma de onda generada, estabilidad y frecuencia de oscilación.


## 6. Entregables

Se requiere la entrega de un informe donde responda cada uno de los apartados teniendo en cuenta simulaciones, especificaciones técnicas de las compuertas utilizadas en esta práctica, mediciones obtenidas en el laboratorio de manera sustentada.

## 7. Referencias

**[1]** Cornell University. (2010). EE 2301 Experiment 3: TTL and CMOS Logic [PDF]. Disponible en: http://www.lns.cornell.edu/~ib38/teaching/p360/lectures/wk09/l26/EE2301Exp3F10.pdf


## 8. Material de apoyo

* [Modelos spice del 74LS04 y CD4069](./spice/).
* [Importar modelos en LTSpice](./spice/LTSpice.md).
* [Vídeo sobre niveles de tensión y corriente para algunas tecnologías de electrónica digital](https://www.youtube.com/watch?v=wCQ2D2S836I).
