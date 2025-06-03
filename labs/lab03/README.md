# Lab03: Decodificador BCD a 7 segmentos

Contenido:

1. [Objetivos de aprendizaje](#1-objetivos-de-aprendizaje)

2. [Fundamento teórico](#2-fundamento-teórico)

3. [Procedimiento](#3-procedimiento)

4. [Entregables](#4-entregables)


## 1. Objetivos de aprendizaje

1. Diseñar e implementar un controlador para display 7 segmentos teniendo en cuenta el tipo de display (ánodo/cátodo común), la tabla de verdad completa para representación hexadecimal y el respectivo mapeo de pines .

2. Desarrollar la descripción de hardware para convertir números binarios  2 dígitos BCD (unidades y decenas) y 1 bit de signo (0 = positivo, 1 = negativo).

3. Visualizar el resultado de un sumador/restador de $4$ bits en los display $7$ segmentos que vienen en la tarjeta de desarrollo.

## 2. Fundamento teórico

### 2.1 BCD (Binary Coded Decimal): 
-------------------------------

BCD significa Décimal Codificado en Binario y representa el sistema de numeración digital en el que podemos representar cada número décimal utilizando 4 bits de números binarios.


Como sabemos hay 10 dígitos en el sistema décimal, para representarlos necesitamos 10 combinaciones de 4 bits binarios.

<p align="center">

|   Dígito  |   Bit $_3$  |  Bit $_2$ |   Bit $_1$  |   Bit $_0$  |
|-----------|-------------|-----------|-------------|-------------|
|     0     |      0      |     0     |      0      |      0      |
|     1     |      0      |     0     |      0      |      1      |
|     2     |      0      |     0     |      1      |      0      |
|     3     |      0      |     0     |      1      |      1      | 
|     4     |      0      |     1     |      0      |      0      |
|     5     |      0      |     1     |      0      |      1      |
|     6     |      0      |     1     |      1      |      0      |
|     7     |      0      |     1     |      1      |      1      | 
|     8     |      1      |     0     |      0      |      0      | 
|     9     |      1      |     0     |      0      |      1      | 
</p>

Ahora bien, también es posible representar de forma binaria los números décimales del 10 al 15 pero empleando su correspondiente representación en el sistema hexadécimal:

<p align="center">

|   Dígito  |   Bit $_3$  |  Bit $_2$ |   Bit $_1$  |   Bit $_0$  |
|-----------|-------------|-----------|-------------|-------------|
|     A     |      1      |     0     |      1      |      0      |
|     B     |      1      |     0     |      1      |      1      |
|     C     |      1      |     0     |      0      |      0      |
|     D     |      1      |     1     |      0      |      1      | 
|     E     |      1      |     1     |      1      |      0      |
|     F     |      1      |     1     |      1      |      1      |
</p>


### 2.2 Display de 7 segmentos:
-------------------------------


El display de siete segmentos es un dispositivo electrónico que consta de siete diodos emisores de luz (LED) dispuestos en un patrón definido; encender una combinación particular de éstos permite representar un dígito décimal o hexadécimal Existen dos tipos de display LED de siete segmentos:

* Tipo de cátodo común: en este tipo de display, todos los cátodos de los siete LEDs están conectados entre sí a tierra o $-Vcc$ (por lo tanto, cátodo común) y el LED muestra dígitos cuando se suministra un nivel alto a los ánodos individuales.
    
* Tipo de ánodo común: en este tipo de display, todos los ánodos de los siete LEDs están conectados a $+Vcc$ (por lo tanto, ánodo común) y el LED muestra dígitos cuando se suministra un nivel al bajo a los cátodos individuales.


En las siguientes figuras se muestra cómo se distribuyen los 7 segmentos en el display cuando se tiene una configuración de ánodo común:

<p align="center">
 <img src="/pics/lab03/segm.png" alt="alt text" width=500 >
</p>


<p align="center">
 <img src="https://exploreembedded.com/wiki/images/1/1a/0SevenSegment.gif" alt="alt text" width=400 >
</p>

## 3. Procedimiento

### Primera parte: Diseño BCD a 7seg

Realizar el diseño, sintentización e implementación del display de $7$ segmentos, que permita visualizar números en representación hexadécimal en uno de los displays de la tarjeta de desarrollo. 


Pasos a seguir:

1. Definir el bloque funcional del diseño:

    <p align="center">
        <img src="/pics/lab03/Sseg.png" alt="alt text" width=350 >
    </p>


    Como se evidencia, el bloque tiene un puerto de entrada  llamado ```BCD``` de 4 bits y un puerto de salida llamado ```Sseg``` de 7 bits, lo que concuerda con lo mencionado anteriormente.

2.  Definir la descripción funcional del diseño: Tablas de verdad.

3. Describir usando HDL el comportamiento del diseño. 

4. Simular el diseño: Implemente un *testbench* para este fin. 

5. Implementación: en la tarjeta correspondiente implemente y valide el funcionamiento.

### Segunda parte: Visualización dinámica en 3 displays de 7 segmentos

Realizar la integración  del módulo implementado en el ítem anterior con el sumador/restador del [lab02](/laboratorios/2_restador/README.md), siguiento los mismo pasos descritos anteriormente. A continuación se muestra el bloque funcional que deben implementar:


<p align="center">
        <img src="/pics/lab03/all.png" alt="alt text" width=750 >
    </p>


#### Representación decimal de números negativos

Cuando el resultado de una resta es negativo (```Co = 0```), el valor de salida (```S```) está expresado en complemento a $2$. Para convertirlo a su equivalente decimal con signo:

* Aplicar complemento a $2$ nuevamente al resultado para obtener su magnitud positiva.

* Agregar un signo negativo al valor obtenido.

Procedimiento detallado:

1. Invertir todos los bits de $S$:

    $$\text{Complemento a } 1 =∼S$$ 
    
2. Sumar $1$ al resultado:
     $$\text{Magnitud positiva } =(∼S)+1$$

3. Asignar signo negativo:
   $$\text{Resultado decimal } =−\text{Magnitud positiva}$$


## 4. Entregables

1. Descripción de hardware del sumador/restador.

2. Documentación del ítem anterior en su respectivo archivo ```README.md```.

3. Realice la respectiva simulaciones y muestre evidencias en su archivo ```README.md```.

4. Implemente la descripción HDL en la tarjeta de desarrollo, empleando la ```IDE Quartus``` y muestre en el laboratorio el funcionamiento, empleando los periféricos que requiera.

