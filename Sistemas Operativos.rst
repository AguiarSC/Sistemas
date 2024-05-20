======================
SISTEMAS INFORMÁTICOS
======================
  
La ``informática`` (información + automática) es la ciencia que utiliza ordenadores para el tratamiento de la información. Los ``datos`` son conjuntos de símbolos que se utilizan para representar diferentes valores, por sí solos no aportan información, es necesario procesarlos. El término ``información`` es sinónimo de conocimiento y depende del receptor.
Un ``sistema informático`` es un conjunto de elementos que están relacionados entre sí y en el que se realizan tareas relacionadas con el tratamiento automático de la información. Está compuesto por ``hardware`` (componentes físicos), ``software`` (componentes lógicos) y ``recursos humanos``.
  
* ``Hardware``
  Compuesto por los elementos físicos, que se pueden tocar. Algunos elementos hardware son la caja, el procesador, la memoria, el disco duro, pantalla, teclado, ratón, etc.

  * ``Procesador (CPU: Central Process Unit)``
    Su función es leer instrucciones y ejecutarlas. Obtiene la primera instrucción de la memoria, la decodifica, la ejecuta y, en algunos casos, almacena el resultado. 

  * ``Memoria``
    Almacena los programas en ejecución y los datos que necesitan. Se organiza en niveles: memoria principal (registros - caché - RAM), memoria secundaria (ROM - discos duros - CD) y memoria auxiliar (nube, hdds y cds de ayuda). Cuanto más cercanos al procesador, más pequeños, rápidos y caros.

  * ``Dispositivos E/S o periféricos``
    Tienen dos partes: dispositivo ``controlador`` y el dispositivo en sí. El controlador es un chip o un conjunto de chips que controlan físicamente el dispositivo. La comunicación entre el controlador y el sistema operativo se realiza mediante un software llamado driver.

* ``Software``
  Es la parte lógica del sistema e intangible, como los programas y los datos. Está formado por un conjunto de instrucciones que al ejecutarse sirven para realizar alguna tarea. Se puede dividir en 3 tipos por la función o en 2 según su tipo.

  * ``Software de sistema``
    Programas que administran los recursos del ordenador; son los sistemas operativos y los drivers.

  * ``Software de programación``
    Cualquier software que permita crear nuevos programas y aplicaciones. Ejemplos: NetBeans..

  * ``Software de aplicación``
    Se utiliza para trabajar con el equipo informático y permiten realizar tareas básicas. Este software se denomina aplicaciones, dentro de las cuales están las de propósito general y las de propósito específico o personalizado

  * ``Software propietario``
    Licencia de pago generalmente, en el que el propietario establece una serie de restricciones sobre él dando lugar a diferentes licencias. Ejemplo: Sistema operativo Windows de Microsoft.

  * ``Software libre``
    Es un software sujeto a una licencia llamada de software libre. La más extendida es la licencia GPL (Licencia General Pública). Dentro del software libre está el concepto de código abierto u open source, que significa que el software se distribuye con el código fuente. Software libre no quiere decir gratis (éste llamado freeware), puede ser comercializado, pero se considera libre porque el usuario tiene libertad para ejecutarlo, estudiarlo, modificarlo, distribuirlo, mejorarlo y compartirlo.


Concepto de sistema operativo
-----------------------------
    
Intermediario entre el usuario y el hardware. Facilita la comunicación y oculta los detalles de funcionamiento mediante una interfaz amigable. Administra los recursos del sistema, lo que permite la ejecución simultánea de múltiples programas que comparten recursos. La interfaz está formada por programas que varían según el S.O.

Para garantizar la seguridad, el software puede ejecutarse en dos modos distintos:

* ``Modo protegido o kernel``: permite el acceso completo al hardware y a los recursos del sistema.
* ``Modo usuario``: restringe la ejecución a un conjunto específico de instrucciones, limitando así el acceso a recursos críticos.
 
Estructura del S.O.
-------------------

* ``Sistemas Monolíticos``: Son simples y ejecutan todas las funciones en un solo programa en modo kernel. Ejemplos incluyen UNIX, Linux, FreeBSD, MS-DOS y Mac OS.
    
* ``Sistemas de Capas o Jerárquicos``: Organizados en capas con funciones específicas, desde hardware hasta procesos de usuario. Ejemplo: THE.
    
* ``Micronúcleo o Microkernel``: Divide el sistema en módulos pequeños para mayor tolerancia a fallos. Ejemplo: Minix.
    
* ``Máquinas Virtuales``: Integración de varios sistemas operativos en una sola máquina.
    
* ``Exokernels``: Particionan recursos de la máquina para asignar a cada usuario. Ejemplo: ExOS y Extended OpenBSD.
    
* ``Modelos Híbridos``: Los sistemas modernos combinan enfoques para mejorar rendimiento, seguridad y usabilidad. Ejemplos incluyen Kernels de Linux y Solaris, así como Windows.

    
Tipos de S.O.
-------------

* ``Número de Usuarios``

  * ``Monousuario``: Un único usuario utiliza el sistema operativo a la vez. Ejemplo: MS-DOS.

  * ``Multiusuario``: Varios usuarios pueden trabajar simultáneamente, ya sea en el mismo ordenador o a través de la red. Ejemplos: Unix, GNU-Linux, Windows Server, Windows 7, Windows 8, Windows 10, etc.

* ``Número de Procesos o Tareas``

  * ``Monotarea o Monoprogramación``: Solo se ejecuta un proceso a la vez. Ejemplo: DOS.

  * ``Multitarea o Multiprogramación``: Múltiples procesos se ejecutan simultáneamente. Ejemplos: UNIX, Linux, Windows NT, XP, Vista, 7, Windows actuales, Mac OS, etc.

* ``Número de Procesadores``

  * ``Monoprocesador``: El sistema operativo funciona solo en ordenadores con un procesador. Ejemplo: basados en MS-DOS.

  * ``Multiprocesador``: El sistema operativo puede utilizarse en ordenadores con varios procesadores. Ejemplos: familia de Windows Server, UNIX, Linux, etc.

* ``Tipo de Dispositivo Utilizado``

  * ``Supercomputadoras y Mainframes``: Procesamiento por lotes y en tiempo compartido.

  * ``Para Servidores``: Proporcionan servicios a través de la red. Ejemplos: Solaris, UNIX, Windows Server, etc.

  * ``Para Ordenadores Personales``: Realizan tareas básicas. Ejemplos: Linux, Windows, Mac OS, etc.

  * ``Para Dispositivos de Bolsillo``: Cada vez más sofisticados. Ejemplos: Android, Blackberry, iOS, etc.

  * ``Para Dispositivos Integrados``: Embebidos para funciones específicas, con un número limitado de funciones. Se encuentran en televisores, coches (sistemas de navegación), consolas de videojuegos, móviles, semáforos, cajeros automáticos, etc.


Función del S.O.
----------------

* ``Gestión de Procesos``: El sistema operativo se encarga de crear, destruir, suspender, reanudar, sincronizar y comunicar procesos, donde un proceso es un programa en ejecución.

* ``Gestión de Memoria``: El sistema operativo gestiona la asignación y liberación de memoria, decide cuánta memoria se asigna a un proceso y controla las partes de la memoria que se están utilizando para almacenar procesos e información.

* ``Gestión de Archivos``: El sistema operativo se encarga de gestionar el almacenamiento de información en los dispositivos.

* ``Gestión de Entrada y Salida``: El sistema operativo captura interrupciones (señales que indican la necesidad de atención inmediata por parte del sistema) de los dispositivos y gestiona la entrada y salida de datos.


Gestión de procesos
-------------------

* Los programas almacenados en dispositivos de almacenamiento se convierten en ``procesos`` cuando se ejecutan.

* Los procesos pueden crearse al arrancar el sistema operativo, por petición de un usuario o cuando un proceso existente crea uno nuevo.

* Los procesos pueden terminar de forma normal, por error, por petición del usuario o por una llamada al sistema.

* Al ejecutarse, el sistema operativo asigna a cada proceso un espacio de direcciones y lo añade a una tabla de procesos (PCB).

* La tabla de procesos contiene información como el identificador del proceso, su estado, prioridad, dirección de memoria, directorio de trabajo y tiempo de uso del procesador.

* Los procesos pueden ejecutarse casi concurrentemente, incluso en sistemas con un solo procesador, dando la sensación de paralelismo.
  

Estados de procesos
-------------------

* Los procesos pasan por distintos estados: ``creación``, ``listo``, ``ejecución`` y ``bloqueado``.

* Cuando se inicia, el proceso se coloca en una ``cola de trabajos``. Estado ``creado``.

* Si es admitido por el sistema, se coloca en una cola de ``procesos listos, esperando para ejecutarse``.

* Cuando se le asigna tiempo de CPU, pasa al ``estado de ejecución``.

* Si necesita algún recurso o se produce un evento que lo interrumpe, pasa al estado ``bloqueado``.

* Los cambios de estado se denominan ``transiciones``.


Gestión de la memoria
---------------------

La gestión eficiente de la memoria principal es crucial para garantizar el rendimiento óptimo del sistema operativo (S.O.) y los procesos que se ejecutan en él. El administrador de memoria se encarga de asignar y liberar la memoria según sea necesario, asegurando un uso eficaz de los recursos disponibles.

En los primeros sistemas operativos, la memoria se dividía en dos partes: una para el sistema operativo y otra para los programas de usuario. Sin embargo, con la evolución actual, el S.O. gestiona múltiples programas asignándoles espacios llamados particiones. Estas particiones pueden ser de tamaño fijo o variable.

* ``Particionado Fijo``: Asigna particiones predefinidas a los procesos, lo que puede resultar en fragmentación interna y desperdicio de memoria.

* ``Particionado Variable``: Permite una asignación más flexible de memoria, pero puede generar fragmentación externa. Se utilizan estrategias como el primer ajuste, el mejor ajuste y el peor ajuste para asignar espacios de memoria.

1. **Primer Ajuste (First Fit)**:
   - Asigna el primer bloque de memoria libre que sea lo suficientemente grande.
   - Es rápido porque encuentra una solución pronto.
   - Puede generar fragmentación externa.

2. **Mejor Ajuste (Best Fit)**:
   - Asigna el bloque libre más pequeño que sea suficientemente grande.
   - Minimiza el desperdicio inmediato de memoria.
   - Es más lento y puede causar fragmentación externa con pequeños fragmentos dispersos.

3. **Peor Ajuste (Worst Fit)**:
   - Asigna el bloque libre más grande disponible.
   - Deja grandes fragmentos para futuras asignaciones.
   - Es más lento y puede dejar grandes fragmentos subutilizados.

Además, se emplean técnicas como la paginación y la segmentación para permitir que los programas se ubiquen de manera no contigua en memoria. La ``paginación`` divide los programas en páginas del mismo tamaño, mientras que la ``segmentación`` los divide en segmentos de tamaño variable. Estas técnicas pueden reducir la fragmentación, aunque también presentan desafíos en la gestión de memoria.

La ``memoria virtual`` es otro mecanismo fundamental que permite ejecutar programas que no caben completamente en la memoria principal. Utiliza un sistema de paginación para cargar solo las partes necesarias de un programa en memoria, mientras que el resto reside en un dispositivo de almacenamiento secundario. El intercambio (swapping) es una técnica asociada que consiste en mover procesos entre la memoria principal y el almacenamiento secundario para optimizar el uso de los recursos.


Gestión de archivos
-------------------

Los sistemas operativos manejan la información mediante sistemas de archivos para superar las limitaciones de la memoria, como la capacidad de almacenamiento limitada y la volatilidad de los datos. Estos sistemas facilitan a las aplicaciones y usuarios la manipulación de unidades de almacenamiento para guardar y recuperar datos.

* Cada sistema operativo utiliza su propio ``sistema de archivos``.

* No hay ``compatibilidad`` entre los sistemas de archivos de diferentes sistemas operativos.

Los sistemas de archivos actúan como una interfaz entre el S.O. y los dispositivos de almacenamiento, gestionando operaciones como escritura, búsqueda, lectura, almacenamiento y eliminación de archivos y directorios.

* ``Archivos Normales``: Contienen cualquier tipo de información. Los archivos tienen un nombre y una extensión que los identifica.

* ``Directorios``: Almacenan información de otros archivos y pueden contener archivos o subdirectorios. Los directorios pueden representar el directorio actual (".") o el directorio padre (".."). Las rutas de directorios pueden ser absolutas (desde la raíz) o relativas (desde el directorio actual).


Sistemas de archivos
--------------------

* ``Windows``

  * ``FAT16``: Utilizado por Windows 95 y 98, heredado de MS-DOS, nombres de archivos con 8 letras.

  * ``FAT32``: Utilizado por Windows NT, 2000, XP y Vista, admite nombres de archivos con 255 letras.

  * ``NTFS``: Utilizado en versiones modernas de Windows, admite 255 caracteres y Unicode.

  * ``ReFS``: Utilizado a partir de Windows 2012 y Windows 10, con mayor resistencia a la corrupción de datos.

* ``Linux``:

  * ``ext2``: Admite particiones de disco de 4TB y ficheros de hasta 2GB.
  
  * ``ext3``: Modificación de ext2 con journaling.
  
  * ``ext4``: Actual sistema de archivos de Linux, eficiente y con límites de tamaño ampliados.
  
  * ``swap``: Sistema de archivos para la partición de intercambio.


Gestión de entrada y salida
---------------------------

* La E/S implica el movimiento de información entre el sistema informático y el exterior.

* El sistema operativo gestiona la E/S y las direcciones de memoria relacionadas.

* Métodos de gestión de E/S:

  * ``E/S Programada``: El procesador ejecuta un programa para controlar las operaciones de E/S, lo que puede provocar tiempos de espera.

  * ``E/S Controlada por Interrupciones``: Las interrupciones indican al procesador que debe atender a un dispositivo, pero pueden generar conflictos.

  * ``E/S con DMA (Acceso Directo a Memoria)``: Un controlador especializado realiza transferencias de datos sin pasar por la CPU, acelerando el proceso y liberando recursos.


Técnicas para Mejorar la Velocidad
----------------------------------

* ``Caching``: Almacena copias de datos frecuentemente utilizados para un acceso más rápido. Es extremadamente rápido ya que los datos se encuentran en la memoria caché del sistema, que es mucho más rápida que la memoria principal o los dispositivos de almacenamiento. Es preferible cuando se necesita un acceso rápido a datos que se utilizan con frecuencia.

* ``Buffering``: Utiliza zonas de memoria (buffers) para almacenar temporalmente datos durante las transferencias entre dispositivos, acoplando velocidades diferentes. Es rápida ya que implica operaciones en la memoria principal del sistema, que es más rápida que los dispositivos de E/S. Se prefiere en situaciones donde se necesita sincronizar el flujo de datos entre dispositivos con velocidades diferentes.

* ``Spooling``: Utiliza un buffer grande en disco para almacenar información de dispositivos de entrada hasta que los dispositivos de salida estén disponibles, evitando cuellos de botella. Es relativamente más lenta debido a que implica operaciones de lectura y escritura en disco, que son más lentas que la memoria principal o la memoria caché. Se prefiere cuando se necesita gestionar grandes cantidades de datos que no pueden procesarse de inmediato y se debe garantizar la disponibilidad constante de los datos de entrada para los dispositivos de salida.

En resumen, el caching es la más rápida, seguida del buffering y el spooling es la menos rápida pero más útil para manejar grandes volúmenes de datos de manera eficiente.
