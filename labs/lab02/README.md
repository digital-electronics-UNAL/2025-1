# Lab 02: Sumador de 1 bit y sumador de 4 bits

Contenido:

1. [Objetivos de aprendizaje](#1-objetivos-de-aprendizaje)

2. [Fundamento teórico](#2-fundamento-teórico)

    2.1 [Parte 1: Sumador de 1 bit](#21-parte-1-sumador-de-1-bit)

    2.2 [Parte 2: Sumador de 4 bit](#22-parte-2-sumador-de-4-bits)


3. [Entregables](#3-entregables)



## 1. Objetivos de aprendizaje

- Diseñar y construir sistemas digitales basados en lógica combinacional, enfocándose en la implementación de sumadores.
- Diseñar, construir e instanciar módulos utilizando lenguajes de descripción de *hardware* (HDL)
- Familiarizarse con el flujo completo de diseño e implementación en *hardware*, desde la especificación inicial hasta la síntesis e implementación en FPGA.
- Aprender a verificar y validar el funcionamiento del diseño en un entorno de simulación, identificando y corrigiendo errores antes de la implementación física en *hardware*.
- Explorar la implementación de diseños digitales en tarjeta de desearrollo basadas en FPGAs.

## 2. Fundamento teórico

### 2.1 Parte 1: Sumador de 1 bit

En diseño digital, un sumador de 1 bit es un circuito combinacional que realiza la suma de dos bits junto con un bit de acarreo de entrada. Es uno de los bloques fundamentales en la construcción de sumadores de mayor tamaño, que son esenciales en operaciones aritméticas dentro de procesadores y sistemas digitales. También se conoce como sumador completo.  A continuación se muestra su respectivo bloque funcional:

<p align="center">
 <img src="/pics/lab02/1bit.png" alt="alt text" width=300 >
</p>
<p align="center">
 Figura 1
</p>

El sumador de 1 bit toma tres entradas: los dos bits que se desean sumar (```A``` y ```B```) y un bit de acarreo de entrada (```Ci```) que puede provenir de una posición menos significativa en un sumador más grande. El circuito produce dos salidas: el bit de suma (```So```) y el bit de acarreo de salida (```Co```).


A continuación se presenta la tabla de verdad del sumador completo de 1 bit.

<p align="center">

|   A  |   B  |  Ci |   Co  |   So  |
|------|------|-----|-------|-------|
|   0  |   0  |  0  | **0** | **0** |
|   0  |   0  |  1  | **0** | **1** |
|   0  |   1  |  0  | **0** | **1** |
|   0  |   1  |  1  | **1** | **0** | 
|   1  |   0  |  0  | **0** | **1** |
|   1  |   0  |  1  | **1** | **0** |
|   1  |   1  |  0  | **1** | **0** |
|   1  |   1  |  1  | **1** | **1** | 
</p>


A partir de la tabla de verdad, mediante **mapas de Karnaugh**, se obtienen las expresiones que definen el sumador de 1 bit, las cuales son:

<p align="center">
<img src="/pics/lab02/karnaugh.png" alt="alt text" width=800 >
</p>

A partir de las expresiones obtenidas se puede construir el siguiente circuito:

<p align="center">
<img src="/pics/lab02/Circuito_sumador.png" alt="alt text" width=600 >
</p>
<p align="center">
 Figura 2
</p>

#### Implementación en HDL

En la descripción de *hardware*, los sumadores de 1 bit pueden implementarse utilizando diferentes enfoques, según el nivel de abstracción deseado.

  * **Implementación estructural**:

    Se definen explícitamente los componentes individuales (AND, OR, XOR) necesarios para calcular la salida de suma (```So```) y el acarreo (```Co```) según las ecuaciones lógicas obtenidas de la tabla de verdad. Esto se puede realizar de dos formas:

    1. Usando operadores lógicos

        * Descripción: Los operadores lógicos son símbolos o funciones que representan operaciones lógicas sobre las señales. En HDL, estos operadores se usan para crear expresiones que definen cómo las señales de entrada se combinan para obtener una salida. Los operadores lógicos más comunes incluyen AND (```&```), OR (```|```), NOT (```~```), XOR (```^```), etc.

        * Ejemplo:
        
          ```
          assign salida = A & B;  // Operador AND
          ```

        * Características:
        Son más abstractos y concisos.
        Se usan dentro de las expresiones lógicas para realizar combinaciones entre señales.
        Pueden operar sobre señales o vectores de bits.
        No están ligados a ninguna implementación física específica. El sintetizador de hardware es el que decide cómo implementarlos en puertas lógicas (AND, OR, etc.) en función de la optimización.

    2. Usando primitivas

        * Descripción: Las primitivas son elementos de hardware básicos predefinidos en un lenguaje de descripción de hardware (HDL). Estos pueden ser puertas lógicas (como AND, OR, NOT), flip-flops, multiplexores, entre otros. En lugar de escribir operaciones lógicas en forma de expresiones, se utilizan estos bloques como componentes predefinidos y directos de un diseño.

        * Ejemplo:

          ```
          and (salida, A, B);  // Primitiva AND
          ```


        * Características:

          Las primitivas son más cercanas al hardware real, pues cada primitiva corresponde a un bloque o componente físico específico.
          Permiten una descripción explícita del diseño usando componentes predefinidos (puertas, registros, etc.).
          En muchos HDL (como Verilog), las primitivas están predefinidas en la biblioteca y pueden ser más eficientes para la síntesis, ya que el sintetizador ya sabe cómo mapearlas a los recursos del hardware físico.


### 2.2 Parte 2: Sumador de 4 bits


Para crear un sumador de 4 bits, se utilizan cuatro sumadores de 1 bit conectados en serie. Así, el acarreo de salida de un sumador de 1 bit se convierte en el acarreo de entrada del siguiente sumador. Cada bit de los dos números que se están sumando se procesa de manera paralela. 

Para construir un sumador de 4 bits utilizando el sumador de 1 bit como módulo base, se debe **instanciar** varios módulos del sumador de 1 bit y conectar sus entradas y salidas de manera que manejen el acarreo entre cada bit.

Un sumador de 4 bits suma dos números de 4 bits (```[3:0] A``` y ```[3:0] B```) y produce una suma de 4 bits (```[3:0] So```) y un acarreo de salida (```Co```). Para lograr esto, se utilizan 4 sumadores de 1 bit, cada uno manejando una posición de la salida ```So``` (0 a 3) y el acarreo hacia la siguiente posición.  A continuación se muestra su respectivo bloque funcional:

![fpga](/pics/lab02/4bit.png)
<p align="center">
 Figura 3
</p>


La implementación del sumador de 4 bits utilizando instancias del sumador de 1 bit es un ejemplo de diseño estructural en HDL, en donde se utiliza el sumador de 1 bit para construir un sumador de 4 bits de manera modular.

#### Funcionamiento

* Cada instancia del sumador de 1 bit toma 1 bits de las entradas ```A``` y ```B```, y un acarreo de entrada Ci. Calcula la suma de estos bits y produce una suma de un bit ```So``` y un acarreo de salida ```Co```.

* El acarreo de salida de un sumador de 1 bit se usa como acarreo de entrada para el siguiente sumador de 1 bit en la cadena.

* El sumador de 4 bits produce una salida final ```So``` de 4 bits y un acarreo de salida final ```Co```.

#### Implementación en HDL

1. **Concepto de instancia**

    En el contexto de diseño digital y descripción HDL, una instancia se refiere a la creación de un módulo a partir de una definición previamente definida. Instanciar un módulo significa utilizar el módulo definido anteriormente como un bloque en un diseño más grande, proporcionando conexiones específicas para las entradas y salidas del módulo.

    En Verilog podemos utilizar la siguiente sintaxis:

    ```
    module_name instance_name(.port_0(signal_0),..,.port_n(signal_n))
    ```


    donde: 

      * ```module_name```: Es el nombre del módulo que queremos instanciar.

      * ```instance_name```: Es el nombre de la instancia que vamos a generar a nivel local.

      * ```port_0``` ... ```port_1```: Representa al nombre del puerto o variable declarada como entrada o salida del módulo que queremos instanciar, es decir, los nombres de los puertos que aparecen en el prototipo de dicho módulo.

      * ```signal_0``` ... ```signal_n```: Corresponde al nombre de las señales que tenemos en el módulo en el cual nos encontramos trabajando y que nos servirán para interactuar con otros del diseño dentro de dicho módulo.


## 3. Entregables

1. Realice la descripción de hardware de las partes 1 y 2 anteriormente mencionadas.

2. Explique el ítem anterior en su respectivo archivo ```README.md```.

3. Realice la respectiva simulaciones y muestre evidencias en su archivo ```README.md```.

4. Implemente la descripción HDL en la tarjeta de desarrollo, empleando la ```IDE Quartus``` y muestre en el laboratorio el funcionamiento, empleando los periféricos que requiera.




