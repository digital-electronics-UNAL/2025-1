# Lab 00: Instalación de herramientas 

En este laboratorio nos enfocaremos en la instalación y configuración de las herramientas esenciales para el desarrollo de este curso.


## 1. *FPGA Design Software* - Quartus (Para síntesis en FPGA Cyclone IV)

Quartus es un software de diseño digital e implementación FPGA desarrollado por Intel (anteriormente Altera). Es ampliamente utilizado para la síntesis, implementación y verificación de diseños digitales en FPGAs de la familia Cyclone.

* [Guía de instalación](/labs/lab00/Quartus_installation_guide.md)

* [Tutorial de implementación en la FPGA Cyclone IV](/labs/lab00/proyectoQuartus.md)

## 2. Herramientas de simulación *Open Source*:

1. ### Icarus Verilog

  Icarus Verilog es una herramienta de simulación de código abierto para HDL (*Hardware Description Language*). Es ideal para simular y verificar diseños digitales antes de su implementación en hardware.

  * [Guía de instalación](/labs/lab00/iverilog.md)

2. ### Digital - Simulador de circuitos

   * [Digital - Simulador de circuitos](/labs/lab00/digital.md)


## 2. Visual Studio Code 

```Visual Studio Code``` (```VS Code```) es un editor de código ligero pero potente, desarrollado por Microsoft. Es altamente personalizable y cuenta con una amplia gama de extensiones que lo hacen ideal para el desarrollo de software y hardware.

1. Descargar Visual Studio Code: [VS Code download](https://code.visualstudio.com/).

2. Seguir las instrucciones del instalador para completar la instalación.

3. Una vez instalado, abrir ```VS Code``` y explora las extensiones disponibles en el marketplace.



## 3. ```Git``` y GitHub

Git es un sistema de control de versiones ampliamente utilizado para gestionar proyectos de software y hardware. GitHub es una plataforma basada en Git que permite alojar repositorios y colaborar en proyectos.

1. Crear cuenta en [GitHub](https://github.com/).

2. Descargar Git en el computador a través del sitio oficial: [Git download](https://git-scm.com/).

3. Seguir las instrucciones del instalador.

4. Configura ```Git``` de acuerdo al nombre de usuario y correo electrónico usados al crear la cuenta en Github:

    En una terminal del sistema operativo ejecutar:

   ```
    git config --global user.name "cuenta de usuario"
    git config --global user.email correo@email.com
    ```

5. Aprender los comandos básicos de Git:

    * ```git init```: Inicializa un repositorio.
    * ```git clone <url>```: Clona un repositorio remoto.
    * ```git add <archivo>```: Añade archivos al área de preparación.
    * ```git commit -m "mensaje"```: Guarda los cambios en el repositorio.
    * ```git push```: Sube los cambios al repositorio remoto.
    * ```git pull```: Actualiza el repositorio local con los cambios remotos.