<h1 align="center">Componentes y estructura de la CPU
<div align="center">

<a href="https://github.com/victordomgs/Teoria-de-sistemas-i-computacion/blob/main/LICENSE"><img src="https://img.shields.io/github/license/abhisheknaiidu/awesome-github-profile-readme?color=2b9348" alt="License Badge"/></a>
<a href="https://agora.xtec.cat/ies-sabadell/"><img src="https://img.shields.io/badge/Institut%20Sabadell-Centre-%23FFD700" alt="Enllaç a Institut Sabadell"/></a>
</a>



</div>

## Contenido:
[1. Introducción a la arquitectura de computadores](#1-introducción-a-la-arquitectura-de-computadores)  

[2. Estructura](#2-estructura)  
  - [2.1. Unidad aritmética lógica](#21-unidad-aritmética-lógica)  
  - [2.2. Unidad de control](#22-unidad-de-control)  
  - [2.3. Memoria interna](#23-memoria-interna)
    - [2.3.1. Especificaciones físicas](#231-especificaciones-físicas)  
    - [2.3.1. Registros](#231-registros)  
    - [2.3.2. Memoria caché](#232-memoria-caché)  
    - [2.3.3. Memoria central](#233-memoria-central)  
  - [2.4. Buses internos](#24-buses-internos)     
  
[3. Funcionamiento](#3-funcionamiento)  
  - [3.1. Instrucciones](#31-instrucciones)  
  - [3.2. Ciclo de instrucciones](#32-ciclo-de-instrucciones)  


# 1. Introducción a la arquitectura de computadores

Von Newman, el año 1945 plantea la **arquitectura básica de las computadoras digitales**. Estas máquinas, eran capaces de ejecutar una serie de instrucciones y ordenes elementales llamadas intrucciones máquina, que quedan almacenadas en lo que se conoce como memoria principal a la espera de ser leídas y ejecutadas por la Unidad Central de Procesamiento. La comunicación de estos dos elementos con el exterior se realiza a través de lo que se conoce como unidad de entrada y salida. 

# 2. Estructura
## 2.1. Unidad aritmética lógica

La **Unidad Aritmética Lógica (UAL)** es la parte del procesador encargada de ejecutar las operaciones matemáticas y lógicas necesarias para el procesamiento de datos. Esta unidad actua en conjunto con la Unidad de Control (UC), que le indica que operaciones tiene que realizar y sobre que operandos. 

Las operaciones básicas que puede ejecutar la UAL son: 
- **Operaciones aritméticas:** suma, resta, multiplicación y división.
- **Operaciones lógicas:** AND, OR, XOR y NOT.
- **Operaciones de desplazamiento:** ya sean operaciones lógicas o aritméticas.
- **Operaciones de comparación:** para determinar relaciones entre nombres. 

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/Teoria-de-sistemas-i-computacion/blob/main/T2-Organizacion-de-computadores/T2.1-Arquitectura-de-computadores/images/Esquema%20de%20ALU.png" alt="Esquema de la ALU" width="670" height="auto"/>
    <p><em>Figura 1: Esquema de la ALU. Fuente: Abacus</em></p>
  </div>

  A continuación, se explican las partes fundamentales de la ALU:

  - **Circuito combinacional:** se encarga de realizar las operaciones con los datos procedentes de los registros de entrada: REN1 y REN2. Las entradas de ordenes que aparecen a la derecha sirven para indicar el tipo de operación necesaria.
  - **Registro de entrada:** se encarga de almacenar los datos y operandos de entrada encargados de realizar la instrucción. También se utilizan para almacenar resultados intermedios o finales de las operaciones.
  - **Registro acumulador:** en este registro se almacenan los resultados de las operaciones realizadas en el circuito combinacional. Y además, esta conectado con el registro de entrada REN2 para poder realizar operaciones concatenadas si es necesario.
  - **Registro de estado:** segun el valor marcado en este registro el procesador ejecutara la operación que más convenga. En realidad, cada uno de los biestables que componen este registro informarán del último valor escrito en el acumulador. Los valores más típicos son los siguientes:

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/Teoria-de-sistemas-i-computacion/blob/main/T2-Organizacion-de-computadores/T2.1-Arquitectura-de-computadores/images/Registro%20de%20estado.png" alt="Registro de estado" width="670" height="auto"/>
    <p><em>Figura 2: Registro de estado. Fuente: Abacus</em></p>
  </div>

  - NU: No utilizado.
  - Z: Indica cuando el resultado es 0. Devuelve 1 cuando este es 0.
  - N: Devuelve 1 cuando el resultado es negativo.
  - C: Biestable indicador de accarreo.
  - O: Biestable indicador de desbordamiento.
  - P: Biestable indicador de paridad.
  - CP: Biestable de acarreo parcial.

## 2.2. Unidad de Control

La **Unidad de Control (UC)** se encarga de la interpretación y ejecución de las instrucciones recibidas desde la memoria principal, así como del control de todos los componentes del sistema. Su función principal es dirigir el funcionamiento de todos los componentes del procesador y coordinar el movimiento de datos entre los diferentes elementos de la CPU y la memoria.

Las funciones esenciales de a UC son: 

- **Contro del flujo de ejecución:** interpreta las instrucciones y las ejecuta en el orden correcto.
- **Generación de señal de control:** envia señales para activar o desactivar los diferentes componentes de la UAL.
- **Gestión de buses de datos y de buses de direcciones:** determina que datos se leen o escriben y hacia donde se deben enviar.
- **Sincronización con el reloj del sistema:** controla el tiempo de ejecución de las instrucciones para mantener el ritmo de trabajo del procesador.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/Teoria-de-sistemas-i-computacion/blob/main/T2-Organizacion-de-computadores/T2.1-Arquitectura-de-computadores/images/Esquema%20de%20la%20UC.png" alt="Esquema de la UC" width="670" height="auto"/>
    <p><em>Figura 3: Esquema de la UC. Fuente: Abacus</em></p>
  </div>

  A continuación, se explican las partes fundamentales de la UC:

  - **Registro de instrucción:** este registro almacena la instrucción que se está ejecutando en este momento, procedente de la memoria principal. Este registro se divide en tres campos:
    - *CO (código de operación):* se encarga de indicar la operación a realizar (suma, resta, multiplicación, etc).
    - *MD (modo de direccionamiento):* se encarga de indicar el modo de acceder a la memoria para buscar el dato o la dirección para ejecutar determinadas instrucciones.
    - *CDE (campo de dirección efectivo):* contiene a información necesaria para que se pueda acceder al dato.
  - **Registro contador de programa (CP):** este registro contiene la dirección de la siguiente instrucción a ejecutar. Al finalizar una instrucción el CP deberá incrementar su valor en uno, con tal de así ejecutar la siguiente instrucción que marque el reloj.
  - **Registro de direcciones de memoria (RDM):** en él se almacenan las direcciones de memoria en las cuales se van a leer o escribir datos.
  - **Registro de datos de memoria (RIM):** almacena temporalmente los datos que se intercambian con la memoria en las operaciones de lectura y escritura.
  - **Decodificador:** es el circuito computacional que toma como entrada los campos CO + MD del registro de instrucciones y activa un conjunto de salidas conectadas directamente como entradas al controlador. Simplifica el trabajo de esté, ya que cada salida del decodificador estará asociada directamente con una instrucción y un modo de direccionamiento determinados, mientras que a su entrada esa misma información está codificada para ahorrar bits de memoria.
  - **Controlador:** este es el verdadero núcleo o cerebro de operaciones del ordenador. Se puede definir como un circuito secuencial, cuyas entradas corresponden a los códigos de operación del repertorio de instrucciones, los modos de direccionamiento de la instrucción a ejecutar y el estado de la máquina, representado por los registros indicadores (flags), y que porpocionan como salida las microórdenes que gobiernan el funcionamiento del ordenador, estas microórdenes son as que activarán las ordenes de lectura o escritura de os registros, las operaciones a realizar en la ALU, la memoria, etc.
    - *Salidas del codificador:* le indican el tipo de instrucción y modo de direccionamiento asociados.
    - *Reloj del sistema:* el controlador debe tener información acerca de los pulsos del reloj para así poder controlar las ordenes.
    - *Registro de estado:* conoce en todo momento el estado de este registro para así poder gobernar adecuadamente las instrucciones de salto. 

El proceso que sigue a la Unidad de Control para ejecutar una instrucción se puede dividir en dos fases principales: 

#### Fase de búsqueda (fetch)

- La UC envía una orden para leer la siguiente instrucción desde la memória central.
- La dirección de esta instrucción esta almacenada en el contrador del programa (CP).
- La instrucción se carga en el registro de instrucciones (RI) y el CP se incrementa para apuntar a la siguiente instrucción.

#### Fase de ejecución (execute)

- La UC interpreta la instrucción cargada en el RI mediante el decodificador.
- Genera las microordenes necesarias para activar la UAL, los registros y los buses según sea necesario.
- Si la operación requiere datos de la memória, las carga al RIM antes de ser procesadas.
- Una vez ejecutada la instrucción, la UC pasa a la siguiente instrucción. 

## 2.2. Memoria interna

La **memoria interna** de un ordenador es la que se encuentra dentro del procesador o en estrecha relación con el. Se encarga de almacenar datos y instrucciones que el procesador necesita de manera inmediata. Esta memoria esta jerarquizada en diferentes niveles para optimizar la velocidad de acceso y la eficiencia del sistema. 

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/Teoria-de-sistemas-i-computacion/blob/main/T2-Organizacion-de-computadores/T2.1-Arquitectura-de-computadores/images/Memoria%20interna.png" alt="Memoria interna" width="670" height="auto"/>
    <p><em>Figura 4: Memoria interna. Fuente: Abacus</em></p>
  </div>

### 2.3.1. Especificaciones físicas

La memoria de un sistema informático se define como el medio físico capaz de almacenar información de forma temporal o permanente. Enta información puede ser leída o escrita según las características de cada tipo de memoria. 

### Características principales

Las características principales de la memoria estan determinadas por los siguientes factores: 

#### Duración de la información

- **Memorias volátiles:** la información se mantiene solo mientras hay suministro eléctrico (por ejemplo, la RAM).
- **Memorias no volátiles:** la información persiste despues de apagar el equipo (por ejemplo, la ROM, o las memorias flash).
- **Memorias permanentes:** no pueden ser modificadas una vez grabadas.
- **Memorias con refresco:** necesitan una operación periódica para evitar la perdida de datos.

> [!NOTE]  
> La **capacidad de almacenamiento** viene determinada por el número de posiciones de almacenamiento y la cantidad de bits por posición.
> Expresada en bytes (B), kilobytes (KB), megabytes (MB), gigabytes (GB), etc.

#### Velocidad

Para evaluar la velocidad de un dispositivo de memoria se utilizan tres parámetros: 

- **Tiempo de acceso (TA):** tiempo necesario para eer o escribir un dato en una posición determinada.
- **Tiempo de ciclo (TC):** tiempo mínimo entre dos operaciones sucesivas sobre la memoria.
- **Frecuencia de acceso (FA):** nombre de lecturas/escrituras que se pueden hacer por unidad de tiempo. 
