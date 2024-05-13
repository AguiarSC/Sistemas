======================
SISTEMAS INFORMÁTICOS
======================
  
La informática (información + automática) es la ciencia que utiliza ordenadores para el tratamiento de la información. Los datos son conjuntos de símbolos que se utilizan para representar diferentes valores, por sí solos no aportan información, es necesario procesarlos. El término información es sinónimo de conocimiento y depende del receptor.
Un sistema informático es un conjunto de elementos que están relacionados entre sí y en el que se realizan tareas relacionadas con el tratamiento automático de la información. Está compuesto por hardware (componentes físicos), software (componentes lógicos) y
recursos humanos.
  
* Hardware
  Compuesto por los elementos físicos, que se pueden tocar. Algunos elementos hardware son la caja, el procesador, la memoria, el disco duro, pantalla, teclado, ratón, etc.

  * Procesador (CPU: Central Process Unit)
    Su función es leer instrucciones y ejecutarlas. Obtiene la primera instrucción de la memoria, la decodifica, la ejecuta y, en algunos casos, almacena el resultado. 

  * Memoria
    Almacena los programas en ejecución y los datos que necesitan. Se organiza en niveles: registros - caché - RAM y ROM - discos duros - memoria auxiliar. Cuanto más cercanos al procesador, más pequeños, rápidos y caros.

  * Dispositivos E/S o periféricos
    Tienen dos partes: dispositivo controlador y el dispositivo en sí. El controlador es un chip o un conjunto de chips que controlan físicamente el dispositivo. La comunicación entre el controlador y el sistema operativo se realiza mediante un software llamado driver.

* Software
  Es la parte lógica del sistema e intangible, como los programas y los datos. Está formado por un conjunto de instrucciones que al ejecutarse sirven para realizar alguna tarea. Se puede dividir en 3 tipos por la función o en 2 según su tipo.

  * Software de sistema
    Programas que administran los recursos del ordenador; son los sistemas operativos y los drivers. Ejemplos: Sistemas operativos.

  * Software de programación 
    Cualquier software que permita crear nuevos programas y aplicaciones. Ejemplos: NetBeans..

  * Software de aplicación
    Se utiliza para trabajar con el equipo informático y permiten realizar tareas básicas. Este software se denomina aplicaciones, dentro de las cuales están las de propósito general y las de propósito específico o personalizado

  * Software propietario
    Licencia de pago generalmente, en el que el propietario establece una serie de restricciones sobre él dando lugar a diferentes licencias. Ejemplo: Sistema operativo Windows de Microsoft.

  * Software libre: es un software sujeto a una licencia llamada de software libre. La más extendida es la licencia GPL (Licencia General Pública). Dentro del software libre está el concepto de código abierto u open source, que significa que el software se distribuye   con el código fuente. Software libre no quiere decir gratis (éste llamado freeware), puede ser comercializado, pero se considera libre porque el usuario tiene libertad para ejecutarlo, estudiarlo, modificarlo, distribuirlo, mejorarlo y compartirlo.


Concepto de sistema operativo
-----------------------------
    
Intermediario entre el usuario y el hardware. Facilita la comunicación y oculta los detalles de funcionamiento mediante una interfaz amigable. Administra los recursos del sistema, lo que permite la ejecución simultánea de múltiples programas que comparten recursos. La interfaz está formada por programas que varían según el S.O.

Para garantizar la seguridad, el software puede ejecutarse en dos modos distintos:

* Modo protegido o kernel: permite el acceso completo al hardware y a los recursos del sistema.
* Modo usuario: restringe la ejecución a un conjunto específico de instrucciones, limitando así el acceso a recursos críticos.
 
Estructura del S.O.
-------------------

* Sistemas Monolíticos: Son simples y ejecutan todas las funciones en un solo programa en modo kernel. Ejemplos incluyen UNIX, Linux, FreeBSD, MS-DOS y Mac OS.
    
* Sistemas de Capas o Jerárquicos: Organizados en capas con funciones específicas, desde hardware hasta procesos de usuario. Ejemplo: THE.
    
* Micronúcleo o Microkernel: Divide el sistema en módulos pequeños para mayor tolerancia a fallos. Ejemplo: Minix.
    
* Máquinas Virtuales: Integración de varios sistemas operativos en una sola máquina.
    
* Exokernels: Particionan recursos de la máquina para asignar a cada usuario. Ejemplo: ExOS y Extended OpenBSD.
    
* Modelos Híbridos: Los sistemas modernos combinan enfoques para mejorar rendimiento, seguridad y usabilidad. Ejemplos incluyen Kernels de Linux y Solaris, así como Windows.

    
Tipos de S.O.
-------------

* Número de Usuarios:

  * Monousuario: Un único usuario utiliza el sistema operativo a la vez. Ejemplo: MS-DOS.

  * Multiusuario: Varios usuarios pueden trabajar simultáneamente, ya sea en el mismo ordenador o a través de la red. Ejemplos: Unix, GNU-Linux, Windows Server, Windows 7, Windows 8, Windows 10, etc.

* Número de Procesos o Tareas:

  * Monotarea o Monoprogramación: Solo se ejecuta un proceso a la vez. Ejemplo: DOS.

  * Multitarea o Multiprogramación: Múltiples procesos se ejecutan simultáneamente. Ejemplos: UNIX, Linux, Windows NT, XP, Vista, 7, Windows actuales, Mac OS, etc.

* Número de Procesadores:

  * Monoprocesador: El sistema operativo funciona solo en ordenadores con un procesador. Ejemplo: basados en MS-DOS.

  * Multiprocesador: El sistema operativo puede utilizarse en ordenadores con varios procesadores. Ejemplos: familia de Windows Server, UNIX, Linux, etc.

* Tipo de Dispositivo Utilizado:

  * Supercomputadoras y Mainframes: Procesamiento por lotes y en tiempo compartido.

  * Para Servidores: Proporcionan servicios a través de la red. Ejemplos: Solaris, UNIX, Windows Server, etc.

  * Para Ordenadores Personales: Realizan tareas básicas. Ejemplos: Linux, Windows, Mac OS, etc.

  * Para Dispositivos de Bolsillo: Cada vez más sofisticados. Ejemplos: Android, Blackberry, iOS, etc.

  * Para Dispositivos Integrados: Embebidos para funciones específicas, con un número limitado de funciones. Se encuentran en televisores, coches (sistemas de navegación), consolas de videojuegos, móviles, semáforos, cajeros automáticos, etc.

Función del S.O.
----------------

* Gestión de Procesos: El sistema operativo se encarga de crear, destruir, suspender, reanudar, sincronizar y comunicar procesos, donde un proceso es un programa en ejecución.

* Gestión de Memoria: El sistema operativo gestiona la asignación y liberación de memoria, decide cuánta memoria se asigna a un proceso y controla las partes de la memoria que se están utilizando para almacenar procesos e información.

* Gestión de Archivos: El sistema operativo se encarga de gestionar el almacenamiento de información en los dispositivos.

* Gestión de Entrada y Salida: El sistema operativo captura interrupciones de los dispositivos y gestiona la entrada y salida de datos.


Gestión de procesos
-------------------

* Los programas almacenados en dispositivos de almacenamiento se convierten en procesos cuando se ejecutan.

* Los procesos pueden crearse al arrancar el sistema operativo, por petición de un usuario o cuando un proceso existente crea uno nuevo.

* Los procesos pueden terminar de forma normal, por error, por petición del usuario o por una llamada al sistema.

* Al ejecutarse, el sistema operativo asigna a cada proceso un espacio de direcciones y lo añade a una tabla de procesos (PCB).

* La tabla de procesos contiene información como el identificador del proceso, su estado, prioridad, dirección de memoria, directorio de trabajo y tiempo de uso del procesador.

* Los procesos pueden ejecutarse casi concurrentemente, incluso en sistemas con un solo procesador, dando la sensación de paralelismo.
  

Estados de procesos
-------------------

* Los procesos pasan por distintos estados: creación, listo, ejecución y bloqueado.

* Cuando se inicia, el proceso se coloca en una cola de trabajos.

* Si es admitido por el sistema, se coloca en una cola de procesos listos, esperando para ejecutarse.

* Cuando se le asigna tiempo de CPU, pasa al estado de ejecución.

* Si necesita algún recurso o se produce un evento que lo interrumpe, pasa al estado bloqueado.

* Los cambios de estado se denominan transiciones.
