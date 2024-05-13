HERRAMIENTAS DE ADMINISTRACIÓN DE DISCOS
========================================

Las particiones son divisiones lógicas del disco duro que se pueden crear para compartir varios sistemas operativos en un mismo disco duro. Cada partición tendría la estructura lógica correspondiente a su sistema operativo instalado. Podemos optar por crear una o varias particiones, pero el espacio asignado a una partición en un disco debe ser contiguo. El espacio del disco que no pertenezca a ninguna partición será espacio sin asignar.

Desde el punto de vista del usuario, cada partición aparece como un disco distinto con el que trabaja de forma independiente, aunque sean particiones de un mismo disco.

La cantidad de particiones del disco duro dependerá de la estructura de esa unidad. Para eso se necesita de un sistema para gestionar particiones, siendo los dos más comunes:

* ``MBR`` (Master Boot Record) o ``MSDOS``: Permite hasta 4 particiones primarias o 3 primarias y 1 extendida que puede contener múltiples unidades lógicas. Solo una partición puede ser activa y cargar el sistema operativo al iniciar. El MBR almacena la tabla de particiones y un pequeño programa de arranque.
* ``GPT`` (GUID Partition Table): No tiene limitaciones en el número de particiones y todas son consideradas primarias. Resuelve las limitaciones de tamaño del MBR y proporciona mayor seguridad y arranque más rápido. Reserva un espacio al inicio del disco para la tabla de particiones y el gestor de arranque, incluyendo un MBR para compatibilidad con BIOS antiguas.


``En Linux, el gestor de arranque predeterminado es GRUB (Grand Unifier Bootloader) y en Windows, el gestor de arranque es Windows Boot Manager.``

   
Las operaciones básicas que se pueden realizar sobre particiones son:

* ``Crear partición``

* ``Formatear partición``

* ``Eliminar partición``

* ``Reducir o extender partición``

En la gestión de E/S, el gran desafío para los sistemas operativos es la diversidad de dispositivos y fabricantes. Linux aborda esto tratando todos los dispositivos mediante una interfaz común: la de un archivo, que se puede abrir, escribir, leer y cerrar.

Por lo tanto, para Linux un dispositivo es un fichero especial (localizado en el directorio ``/dev`` que cuelga del directorio raíz) que en realidad enlaza con el controlador del dispositivo. Así, el fichero ``mem`` representa la memoria, ``hdxx`` los dispositivos IDE, ``lp`` las impresoras por el puerto paralelo, etc. La única diferencia posible entre los dispositivos es que pueden ser de dos tipos: de bloque (ej.: disco duro) o de carácter (ej.: ratón, teclado).

Cada unidad de almacenamiento del ordenador y cada posible partición de esta unidad es considerada como un dispositivo:

- ``/dev/hda``, ``/dev/hdb``: Unidades IDE maestro y esclavo del primer canal (controladora principal).
- ``/dev/hdc``, ``/dev/hdd``: Unidades IDE maestro y esclavo del segundo canal (controladora secundaria).
- ``/dev/sda``, ``/dev/sdb``, …, ``/dev/sdh``: Interfaz para discos SCSI, SATA y unidades de conexión USB (unidades FLASH o discos duros externos).
- ``/dev/hda1``, ``/dev/hda2``, … ``/dev/sda1``, ``/dev/sda2``: Particiones dentro de la unidad correspondiente.
- ``/dev/fd*``: Disqueteras.
- ``/dev/scd*`` (también conocida como ``/dev/sr*``): CD-ROM SCSI o DVD
- ``/dev/tty*``: consolas o terminales físicos.

``Con la llegada de SATA, en la actualidad se utiliza mayormente ``sda`` en lugar de ``hda`` para referirse a discos duros. Donde ``sd`` quiere decir serial drive.``
``Por lo menos una partición será asignada al directorio raíz, y el resto de las particiones y unidades se montarán sobre este sistema de ficheros.``


.. _Particiones Linux:

PARTICIONES LINUX
=================

Las particiones que el S.O. Linux instala con las opciones por defecto son:

- ``EFI System Partition``: partición del sistema de arranque de tipo ``FAT32`` y con el punto de montaje ``/boot/efi``
- ``Partición del sistema`` de tipo ``ext4`` con el punto de montaje ``/``. Si se elige este punto de montaje significa que todo el sistema de archivos se cargará en esta partición.

Para sistemas más avanzados, y por seguridad es recomendable tener varias particiones con diferentes puntos de montaje.

.. _Tipos de particionado:


TIPOS DE PARTICIONADO
---------------------

Antes de poder particionar un disco duro tenemos que elegir el tipo de particionado que va a utilizar: ``MBR`` (Master Boot Record) o ``MSDOS`` y ``GPT`` (GUID Partition Table)

Una vez seleccionado el tipo, en la creación de una partición debemos indicar:

- ``El tamaño``
- ``El sistema de archivos de dicha partición``
- ``Si es la partición activa, que será la partición en la que en el momento del arranque el ordenador buscará un gestor de arranque que permita iniciar un sistema operativo.``

.. _Sistema de archivos:


SISTEMAS DE ARCHIVOS
-------------------

El sistema de archivos permite al sistema operativo controlar cómo se lee y escribe la información en los dispositivos de almacenamiento (discos duros, pendrive, tarjetas sd, ...).

Cada sistema operativo trabaja preferiblemente con unos sistemas de archivos determinados. Linux soporta un gran número de sistemas de ficheros de otros sistemas operativos, gracias al ``Sistema de Ficheros Virtual`` (SVF).

.. _Ejemplo de particionado:

.. _Flags de una partición:


FLAGS DE UNA PARTICIÓN
----------------------

Cada partición además puede tener una serie de ``flags`` (se configuran como activado o desactivado con el gestor de particiones Gparted) con los que se ajustan atributos adicionales con los que se indican usos específicos de las particiones.

Son varios los flags que podemos encontrar, pero los más típicos son:

* ``boot``: Flag para indicar que se trata de una partición de arranque porque tiene un sistema operativo

* ``root``: La utilizan los sistemas operativos Linux para saber la partición en la que semonta el raíz del sistema de archivos (/)

* ``swap``: La utilizan los sistemas operativos Linux para saber la partición que se utiliza como swap

* ``raid``: Flag para indicar que esta partición forma parte de una configuración de almacenamiento RAID

* ``hidden``: Flag de partición oculta para particionado MBR

* ``msftdata`` y ``msftres``: Son flags utilizados para particiones específicas de los sistemas Windows (NTFS, FAT32 y exFAT), msftdata para particiones que no tienen el flag boot y msftres para particiones “reservadas”, pero sólo en particionado GPT 

.. _Gestores de particiones:


GESTORES DE PARTICIONES
-----------------------

El particionado de un disco se realiza con unas utilidades de disco llamadas gestores de particiones.

- En Windows (de servidor o escritorio) disponemos de dos gestores de particiones:
  - ``Administración de discos``: Gestor de particiones en modo gráfico
  - ``Diskpart``: Gestor de particiones desde consola

- En Linux disponemos de múltiples herramientas:
  - ``fdisk``: Un gestor de particiones de consola presente en casi todas las distribuciones Linux
  - ``cfdisk``: Un gestor de particiones de consola que incorpora las funcionalidades de fdisk pero con una interfaz que facilita
  - ``parted`` y ``Gparted``: Un gestor de particiones de consola que también dispone de un gestor gráfico y que viene preinstalado en múltiples distribuciones


CREAR Y FORMATEAR PARTICIÓN
============================

Recordamos la nomenclatura de discos y particiones en LINUX:

- Los discos vienen especificados en nomenclaturas /dev/sda, /dev/sdb, /dev/sdc, … en función de la cantidad de discos que dispongamos.
  - ``dev`` → es la abreviatura de device
  - ``sd`` → Es la abreviatura de SCSI mass-storage driver
  - ``a, b, c, ...`` → Es la parte que nos distingue cada disco (a es el disco 1, b el disco 2, c el disco 3, …)

- Las particiones se identifican para cada disco añadiendo el número de partición al final.
  - ``/dev/sda`` → /dev/sda1, /dev/sda2, …
  - ``/dev/sdb`` → /dev/sdb1, /dev/sdb2, …

- Cada disco y partición además tienen el identificador único ``UUID`` (Universally Unique Identifier) que podemos consultar con el comando ``blkid (/sbin/blkid)``, (podemos ver el nombre de dispositivo de bloque, el UUID, el tipo de sistemas de archivos)


FDISK
-----

La herramienta fdisk permite listar y modificar la tabla de particiones de un disco. Para listar todos los discos detectados y sus particiones se ejecuta: ``fdisk -l``. Para listar la tabla de particiones del disco ``/dev/sda`` se ejecuta: ``fdisk -l /dev/sda``. Para ejecutar el comando hay que pasarle como argumento el disco sobre el que se desea trabajar (/dev/sda, /dev/sdb, etc.). El comando a ejecutar es: ``fdisk <disco>``

Funciona como un intérprete de comandos, en modo interactivo, en el que los subcomandos más importantes son:

* ``m (man)``: imprime la ayuda.

* ``p (print)``: imprime la tabla de particiones del dispositivo.

* ``d (delete)``: eliminar partición.

* ``n (new)``: crea una nueva partición.

* ``q (quit)``: salir sin guardar los cambios.

* ``w (write)``: escribir los cambios y salir.

Para crear una nueva partición se elige la letra "n".
Se le da formato a la partición con el comando ``mkfs (make filesystem)``. Actualmente, en GNU/Linux existe un programa separado por cada tipo de sistema de ficheros: ``mkfs.ext2, mkfs.ext3, mkfs.ext4, mkfs.ntfs, mkfs.xfs, mkfs.msdos, mkfs.fat, mkfs.vfat`` (es un alias de mkfs.fat), etc. De esta forma mkfs es solamente un front-end que ejecuta el programa apropiado dependiendo del tipo de sistema de ficheros especificado; lo cual haremos con la opción ``-t`` de mkfs.

El comando más básico para la creación de un sistema de archivos FAT es ``mkfs.fat``. Con la opción ``-F`` podemos seleccionar el tamaño de la FAT (File Allocation Table), entre ``12``, ``16`` o ``32``, es decir, entre ``FAT12``, ``FAT16`` o ``FAT32``. Si no se especifica, mkfs.fat seleccionará la opción apropiada según el tamaño del sistema de archivos (consultar man mkfs.fat)

``sudo mkfs.fat -F 32 /dev/sda1``

Por lo tanto, será necesario indicar el tipo de sistema de ficheros y la partición que se quiere formatear. Para formatear una partición el dispositivo ha de estar desmontado.

``mkfs -t ext4 /dev/sdXY o haciendo mkfs.ext4 /dev/sdXY``

También se podrían indicar otras opciones; como etiquetas, formato rápido, tamaño del clúster, etc. Estas opciones varían según el constructor, al que llama mkfs (ver man para mayor detalle).

Para preparar una partición como área de intercambio de memoria virtual se utiliza el comando mkswap

* Preparar partición: mkswap /dev/sdXY

* Habilitar partición de intercambio: swapon /dev/sdXY

* Deshabilitar partición de intercambio: swapoff /dev/sdXY

* Usarla de forma permanente (fichero /etc/fstab): /dev/sda2 none swap sw 0 0

Para poder usar un dispositivo de almacenamiento es necesario montarlo. Antes de montar la partición es necesario crear la carpeta en donde se va a montar. Generalmente en /media o en /mnt. Se ejecutaría el comando: mkdir /media/<nombre_carpeta>

Para acceder a las particiones se usa el comando mount que permite hacer accesible cualquier sistema de archivos reconocible por el núcleo de Linux en un punto de montaje del sistema. Todos los sistemas de archivos se montan directamente por nosotros o indirectamente durante el arranque del sistema, a excepción del sistema de archivos raíz "/", que se asocia a un punto de montaje compilado en el propio kernel y que monta la partición específica durante la instalación.

La carpeta en la que se enlaza el sistema de ficheros se denomina punto de montaje porque es el punto en el que estará accesible el sistema de ficheros.

El formato del comando será: mount [-avwr][-t <sistema_archivos>] /dev/<partición> <carpeta_montaje> siendo todos los parámetros opcionales:

* ``-a``: monta los sistemas de archivos presentes en /etc/fstab, salvo que se indique el parámetro noauto, que impediría el montaje por esta opción.

* ``-v``: muestra información del proceso de montaje

* ``-w``: monta el sistema de archivos con permisos de lectura y escritura.

* ``-r``: monta el sistema de archivos con permisos de solo escritura

* ``-t <sistema_archivos>``: sistema de archivos de la partición para montar (vfat (FAT16 y FAT32), ntfs (NTFS), ext2, ext3, ext4, iso9660, etc.). ES OPCIONAL

* ``/dev/<partición>``: identificador de la partición a montar (hdXY para un disco IDE o ATA, sdXY disco SATA). Para comprobar las particiones existentes se ejecuta: sudo fdisk -l o ls /dev/sd*

* ``<carpeta_montaje>``: donde se montará la partición, es decir, donde aparecerán los datos de la partición. Generalmente en /media o /mnt, aunque puede estar en cualquier otro lugar.

Ejemplos:

* Acceder a un disco ext4 desde la carpeta /media/disco: ``mount -t ext4 /dev/sdXY /media/disco``

* Otros sistemas: ``mount -t ntfs /dev/sdXY /media/Windows``

* Pendrive: ``mount -t vfat /dev/sdXY /media/usb``

* Cdrom: ``mount -t iso9660 /dev/sr0 /media/cdrom``

El sistema mantiene una lista actualizada de sistemas de archivos montados a través de ``/proc/self/mounts``, que se actualiza al montar y desmontar sistemas de archivos. Se pueden listar todas las particiones montadas con el comando ``mount``. Para desmontar una partición, se deshace el vínculo entre la partición y la carpeta de acceso utilizando ``umount /dev/sdXY`` o ``umount /mnt``. Es importante desmontar una partición, especialmente si se han escrito datos, para evitar la pérdida de información. Al desmontar el dispositivo, se vuelcan todas las cachés de escritura al dispositivo.

Las particiones montadas con ``mount`` no se conservan después de reiniciar el sistema. Para montar una partición de forma permanente, se debe agregar una entrada en el archivo ``/etc/fstab``. Durante el arranque, se leen las entradas de este archivo y se montan automáticamente para que estén accesibles a los usuarios.


===============================
CONFIGURACIÓN DEL ARCHIVO FSTAB
===============================

El fichero ``fstab`` (file systems table) se encuentra en el directorio ``/etc`` como parte de la configuración del sistema. Lo más destacado de este fichero es la lista de discos y particiones disponibles. En ella se indica cómo montar cada dispositivo y qué configuración utilizar. Para configurar el archivo fstab es necesario tener permisos administrativos. La información del fichero dependerá del tipo y de la cantidad de dispositivos que existan en el ordenador.

Cada línea tiene seis columnas (``<file system> < mount point > <type> <options> <dump> <pass>``), cuyo significado se detalla a continuación:


* ``file system``: lugar donde se encuentra el dispositivo físico a montar. Será una partición del tipo /dev/sdXY pero también puede ser un archivo o un recurso compartido a través de la red. Se puede utilizar el UUID de la partición.

* ``mount point``: punto de montaje donde será montado el dispositivo físico, es decir carpeta en la que va a estar accesible el sistema de ficheros.

* ``type``: tipo de archivo con el que será montado el dispositivo físico, es decir formato del sistema de ficheros: ext2, ext3, ext4, ntfs, vfat ...

* ``options``: opciones de montaje, parámetros adicionales, pasados como una lista separada por comas. Se puede montar para sólo lectura (ro), o en modo lectura y escritura (rw). Permitir a cualquier usuario montar el sistema de ficheros (user) o sólo usuarios del grupo users (users) o sólo el usuario root puede montar el sistema de ficheros (nouser). Si se quiere que no monte automáticamente la partición en el inicio se puede utilizar noauto. Si se desea utilizar las opciones predeterminadas según el sistema de archivos se puede poner defaults (que son rw, suid, dev, exec, auto, nouser, async). Existen algunas opciones comunes, y otras que dependen del sistema de ficheros al que se quiere acceder.

* ``dump``: utilizado por la herramienta dump para realizar copias de seguridad de las distintas particiones. Normalmente no se encuentra instalado, por lo que la opción más común es 0 (deshabilitado). Con valor 1, dump hace una copia de seguridad del sistema de archivos.

* ``pass``: establece el orden en el que se comprobará/chequeará el sistema de archivos en el arranque. Si ponemos 0 no se comprueba en el arranque. El 1 (comprobar en primer lugar) se reserva para el sistema raíz (/), con 2 se comprobaría en segundo lugar. (Utilizado por el comando fsck (file system consistency check) para controlar el orden en el que son comprobadas las particiones).


===================
ALMACENAMIENTO RAID
===================

RAID (Redundant Array Of Independent Disks) es un término que se refiere a un ``conjunto de discos que se pueden combinar de forma que trabajamos con estos como si fueran un único disco``. Las configuraciones de almacenamiento RAID son más típicas de entornos de servidor, aunque cada vez son más comunes en equipos de escritorio. Dependiendo del modelo de RAID que apliquemos podemos obtener ventajas como:

* Mejorar la integridad de los datos

* Mejorar la tolerancia a fallos y errores en los discos

* Mejorar el rendimiento (velocidad de transferencia)

* Facilitar el aprovechamiento de varios discos (capacidad total de almacenamiento)

A nivel de RAID ``la información se organiza en porciones de tamaño fijo llamadas bandas o stripes``. El tamaño de estas bandas típicamente es de de ``64 Kb`` o ``128 Kb``. Hay distintos tipos de RAID, cada uno con sus características que priman alguno de los aspectos mencionados antes, y que cambian en la forma en la que usan los discos que los forman. 

------------------------------------------------
¿CÓMO SE MEJORA CON RAID LA TOLERANCIA A FALLOS?
------------------------------------------------

Algunas configuraciones RAID replican los datos en varios discos para evitar la pérdida de datos en caso de fallo de un disco. Los sistemas RAID alertan sobre fallos de disco y permiten su reemplazo, replicando los datos en el nuevo disco. ``La tolerancia a fallos está garantizada si no fallan más de un disco a la vez y si se reemplaza y replica un disco antes de que falle otro``. Sin embargo, la replicación reduce el espacio de almacenamiento total del RAID respecto a la suma de las capacidades de los discos. Los sistemas RAID mejoran el rendimiento distribuyendo datos entre discos y acelerando la lectura y escritura. Los discos SSD son preferibles a los discos mecánicos, y la fragmentación puede afectar negativamente al rendimiento.

----------------------------
CONFIGURACIONES RAID BÁSICAS
----------------------------

Para establecer esta configuración, se puede realiza ``mediante software`` (propio o no del sistema operativo) o ``mediante hardware`` específico para el control del RAID (tarjeta de expansión controladora o chipset de la placa base). ``Esta última es la opción más óptima en cuanto a rendimiento``, y con estas podremos utilizar un RAID para la instalación de un sistema operativo, algo que no es posible con las soluciones RAID por software. Si implementamos RAID por software tenemos varias opciones:

* Herramientas RAID en Windows

   * Administración de discos

   * Diskpart

   * Espacios de almacenamiento

   * Grupos de almacenamiento en Windows Server

* Herramientas RAID en Linux

   * LVM (Logical Volume manager)

   * MDADM (Multi Device Administrator)

La forma de realizar un nivel RAID es distribuyendo o redundando los datos entre varios discos de diferentes maneras. Es frecuente emplear el término ``JBOD`` (Just a Bunch of Disks) o ``RAID lineal`` al método de combinar diferentes discos físicos en un solo lógico. JBOD, por tanto, no presenta redundancia ni mejora el rendimiento del conjunto, sin embargo, el tamaño global es la suma de todos ellos.

-------------
TIPOS DE RAID
-------------
* ``RAID 0`` (Data Stripping)
   Se encarga de dividir o distribuir los datos entre dos o más discos sin duplicar la información, es decir, no existe redundancia de datos. Es una configuración que prima la velocidad de lectura y escritura por encima de la tolerancia a fallos, no mejora la seguridad de los datos, solo afecta al rendimiento.

* ``RAID 1`` (Data Mirroring) 
   Emplea un mínimo de dos discos del mismo tamaño o porciones de estos iguales en los que son una copia el uno del otro (aunque aparecen como una única entidad), de ahí el término espejo (mirroring). Esto permite aumentar la fiabilidad de los datos al quedar estos
   duplicados en tantos discos como se desee. Además aumenta la velocidad de lectura.

* ``RAID 5`` (Stripping con paridad distribuida)
   Al igual que RAID 0, realiza una distribución de los bloques de datos, y además genera información de paridad (calculada operando con el resto de datos de la misma división) que se distribuye en todos los discos (al menos tres). Los bloques de paridad permiten reconstruir un disco en caso de fallo sin necesidad de duplicar su almacenamiento. Para ello, han de realizar cálculos de los datos, generando dicha paridad, también llamada código de detección de error o CRC. De este modo, no se desaprovecha tanto espacio redundante, como RAID 1, y además mejora la velocidad de lectura, si bien las escrituras son más costosas al tener que generar códigos CRC y sólo soporta el fallo de un único disco. El espacio útil es la suma de las capacidades de todos los discos menos 1.

* ``RAID 6`` (Stripping con paridad distribuida y duplicada)
   Es como el RAID 5 pero añadiendo un disco adicional para mantener la duplicado. En este caso requiere un mínimo de cuatro discos, siendo así el espacio útil la suma de todos los discos menos dos. Como ventaja tiene la recuperación de datos y como desventaja es que es más lento que el RAID 5 al tener que escribir doble paridad.

-------------------------------------------------
COMBINACIONES RAID: RAID 1+0, RAID 0+1 Y RAID 5+0
-------------------------------------------------

También se pueden establecer combinaciones de niveles RAID anidando es aprovechando las ventajas de varias configuraciones. Así, destacamos los siguientes niveles anidados:

* ``RAID 01``. Consiste en crear dos RAID 0 iguales y sobre estos hacer un RAID 1.

* ``RAID 10``, invierte el orden haciendo primero dos o más RAID 1 y, sobre estos, después hacer un RAID 0.

* ``RAID 50``, se crean dos o más configuraciones iguales de RAID 5 que proporcionan la redundancia de datos y por encima de estas se monta el RAID 0 que proporciona el reparto de los datos para mejorar el rendimiento.

En las RAID con redundancia podemos utilizar un disco de reserva o spare que permanecerá sin utilizar hasta que se produzca un fallo en uno de los discos, momento en el que automáticamente ocupará el sitio del disco erróneo y empezará el proceso de reconstrucción.

Para esto hay dos configuraciones:

* ``Hot Spare``: El disco está conectado y preparado (instantáneamente entra a funcionar).

* ``Standby spare``: El disco está en espera (tarda unos instantes al tener que arrancar).

Si es un standby spare conlleva un proceso de reconstrucción durante la incorporación del disco spare sustituyendo al disco fallido sin embargo si es un hot spare este tiempo se minimiza. El uso de un disco de reserva no ofrece ninguna ventaja de velocidad pero reduce el tiempo de replicación al sustituir automáticamente el disco defectuoso y empezar la reconstrucción de datos justo cuando se produce el error, simplificando las tarea de mantenimiento.

Otra forma de montar un RAID con disco de reserva en modalidad Hot Spare pero sin tener que agregar otro disco adicional es reservar un espacio en los discos del RAID que no se utilizará salvo que se produzca el fallo en uno de ellos, que será el momento en el que la información del disco fallado se replicará en este espacio libre. Esta es la configuración
utilizada por ejemplo en ``RAID 5E`` y ``RAID 6E``, que reservan este espacio de spare al final de los discos paridad. 


======================
ADMINISTRACIÓN DE RAID
======================

La administración de RAID en Linux se realiza con el paquete **mdadm** (Multiple Device Administrator), que se instala con ``sudo apt-get install mdadm``. Antes de iniciar, se puede verificar la existencia de dispositivos RAID en el sistema con ``/proc/mdstat``. La creación de RAID puede realizarse en dispositivos o particiones, no necesariamente del mismo tamaño. En caso de diferencias de tamaño, mdadm advertirá y utilizará el tamaño más pequeño. Los comandos comunes para gestionar RAID en Linux incluyen la creación, establecimiento de dispositivos defectuosos, eliminación, adición, y verificación del estado.

CREACIÓN DE RAID
----------------

.. code-block:: bash

   mdadm --create /dev/mdX --level=Y --raid-devices=Z dispositivos

Donde:

- ``create /dev/mdX`` indica la creación del multidispositivo, siendo X un número.
- ``level=Y`` es el nivel RAID para aplicar, pudiendo ser Y:
  - ``linear`` para RAID lineal
  - ``raid0``, ``0`` o ``stripe`` para RAID0
  - ``raid1``, ``1`` o ``mirror`` para RAID1
  - ``raid5`` o ``5`` para RAID5
  - ``raid6`` o ``6`` para RAID6
  - ``raid10`` o ``10`` para RAID10
- ``raid-devices=Z dispositivos``, donde Z indica el número de dispositivos asociados al RAID y cada uno de ellos separado por espacios (``/dev/sdX /dev/sdY…``).

Establecer un disco como defectuoso de un RAID
----------------------------------------------

.. code-block:: bash

   mdadm /dev/mdX --fail /dev/sdY

Eliminar un disco de un RAID
----------------------------

.. code-block:: bash

   mdadm /dev/mdX --remove /dev/sdY

Añadir un disco a un RAID
-------------------------

.. code-block:: bash

   mdadm /dev/mdX --add /dev/sdY

Comprobar el estado de todos los multidispositivos
-------------------------------------------------

.. code-block:: bash

   cat /proc/mdstat

Obtener información de configuración de todos los multidispositivos
------------------------------------------------------------------

.. code-block:: bash

   mdadm --detail --scan

Obtener información de configuración y construcción de un multidispositivo
-------------------------------------------------------------------------

.. code-block:: bash

   mdadm --detail /dev/mdX
   mdadm --detail /dev/mdX --scan

Examinar el estado de un dispositivo asociado a un RAID
-------------------------------------------------------

.. code-block:: bash

   mdadm --examine /dev/mdX

Detener un RAID
---------------

.. code-block:: bash

   mdadm --stop /dev/mdX

Eliminar el superbloque de un dispositivo (almacena información para manipularlo) sobreescribiendo ceros
--------------------------------------------------------------------------------------------------------

.. code-block:: bash

   mdadm --zero-superblock /dev/sdY


Una vez creado un RAID con ``mdadm`` lo particionamos empleando los métodos tradicionales como ``fdisk``, ``cfdisk``, ``parted`` o ``gparted``, y lo montamos con ``mount``.

Si deseamos eliminar un multidispositivo RAID, debemos:

* Desmontar el dispositivo si está en uso.

* Detener el multidispositivo (ejemplo: ``sudo mdadm --stop /dev/md0``)

* Borrar el superbloque de cada dispositivo que constituía el RAID (es decir borrar el sector 0 de los discos utilizados) (ejemplo: ``sudo mdadm --zero-superblock /dev/sde1``, ``sudo mdadm --zero-superblock /dev/sdd1`` y ``sudo mdadm --zero-superblock /dev/sdg1``)

* En caso de que estuviese asociado al arranque del sistema, actualizar ``/etc/fstab`` eliminando la línea asociada y actualizar initramfs (sistema de archivos RAM de inicio en Linux).
