Herramientas de administración de discos
========================================

Las particiones son divisiones lógicas del disco duro que se pueden crear para compartir varios sistemas operativos en un mismo disco duro. Cada partición tendría la estructura lógica correspondiente a su sistema operativo instalado. Podemos optar por crear una o varias particiones, pero el espacio asignado a una partición en un disco debe ser contiguo. El espacio del disco que no pertenezca a ninguna partición será espacio sin asignar.

Desde el punto de vista del usuario, cada partición aparece como un disco distinto con el que trabaja de forma independiente, aunque sean particiones de un mismo disco.

La respuesta sobre cuántas particiones puede tener el disco duro dependerá de la estructura de esa unidad. Para eso necesitarás de un sistema para gestionar particiones. Hay múltiples tipos de particionado, los dos más comunes son:

* ``MBR`` (Master Boot Record) o ``MSDOS``: un disco duro puede tener hasta 4 particiones primarias. También puede tener tres primarias y una extendida. La extendida estará compuesta por tantas unidades lógicas como alcance la capacidad del disco (máximo de 32). De las 4 particiones, solo una puede estar definida como activa. Será la que cargue el S.O. cuando se inicie el ordenador. En el primer sector del disco duro se sitúa una tabla de particiones, en una zona llamada MBR (Master Boot Record), ésta incluye toda la configuración de particiones del disco duro; las particiones que hay y su tamaño y un pequeño programa que permite localizar la partición activa, leer su sector de arranque y usarlo para arrancar el sistema informático. Además, el MBR reserva espacio para almacenar las instrucciones del gestor de arranque (boot manager).

El gestor de arranque es el primer programa que se ejecuta justo después de las instrucciones de arranque de la BIOS, y este básicamente se encarga de indicar qué partición tiene las instrucciones para arrancar un sistema operativo, redireccionando el arranque a ésta. En el caso de que tengamos múltiples sistemas operativos instalados en un mismo ordenador, un gestor de arranque puede configurarse para mostrar un menú en el que podremos seleccionar el que queremos arrancar. No siempre tendremos un gestor de arranque en el MBR.

* ``GPT`` (GUID Partition Table): En el sistema GPT, las particiones son casi ilimitadas sin importar su relevancia. No hay distinción entre particiones, todas se consideran primarias. En Windows se limita a 128 mientras que GNU/Linux llega a 256. Además, también pueden tener mayor tamaño. Vino a solucionar el problema de las limitaciones de 2 TiB por partición y de 4 TiB por disco del MBR, y tiene mayor seguridad en los datos y arranque más rápido que MBR. Reserva también un espacio al principio del disco donde almacena la tabla de particiones y el gestor de arranque. Este espacio es mayor que en MBR ya que al poder particionar en más trozos necesita más espacio para guarda los datos de todas las particiones. Dentro de este espacio reserva el primer sector (LBA 0) para el también llamado MBR por compatibilidad con equipos con BIOS antiguas.


``En Linux, el gestor de arranque predeterminado es GRUB (Grand Unifier Bootloader) y en Windows, el gestor de arranque es Windows Boot Manager.``

   
Las operaciones básicas que se pueden realizar sobre particiones son:

- ``Crear partición``
- ``Formatear partición``
- ``Eliminar partición``
- ``Reducir o extender partición``

El gran problema que tiene que afrontar el S.O. para gestionar los distintos dispositivos de E/S es la gran cantidad de dispositivos y fabricantes que existen. Linux resuelve este problema tratando todos los dispositivos siguiendo una interface común: la de un fichero, que se puede abrir, escribir, leer y cerrar.

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

Particiones Linux
=================

Las particiones que el S.O. Linux instala con las opciones por defecto son:

- ``EFI System Partition``: partición del sistema de arranque de tipo ``FAT32`` y con el punto de montaje ``/boot/efi``
- ``Partición del sistema`` de tipo ``ext4`` con el punto de montaje ``/``. Si se elige este punto de montaje significa que todo el sistema de archivos se cargará en esta partición.

Para sistemas más avanzados, y por seguridad es recomendable tener varias particiones con diferentes puntos de montaje.

.. _Tipos de particionado:

Tipos de particionado
---------------------

Antes de poder particionar un disco duro tenemos que elegir el tipo de particionado que va a utilizar: ``MBR`` (Master Boot Record) o ``MSDOS`` y ``GPT`` (GUID Partition Table)

Una vez seleccionado el tipo, en la creación de una partición debemos indicar:

- ``El tamaño``
- ``El sistema de archivos de dicha partición``
- ``Si es la partición activa, que será la partición en la que en el momento del arranque el ordenador buscará un gestor de arranque que permita iniciar un sistema operativo.``

.. _Sistema de archivos:

Sistema de archivos
-------------------

El sistema de archivos permite al sistema operativo controlar cómo se lee y escribe la información en los dispositivos de almacenamiento (discos duros, pendrive, tarjetas sd, ...).

Cada sistema operativo trabaja preferiblemente con unos sistemas de archivos determinados. Linux soporta un gran número de sistemas de ficheros de otros sistemas operativos, gracias al ``Sistema de Ficheros Virtual`` (SVF).

.. _Ejemplo de particionado:

.. _Flags de una partición:

Flags de una partición
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

Gestores de particiones
-----------------------

El particionado de un disco se realiza con unas utilidades de disco llamadas gestores de particiones.

- En Windows (de servidor o escritorio) disponemos de dos gestores de particiones:
  - ``Administración de discos``: Gestor de particiones en modo gráfico
  - ``Diskpart``: Gestor de particiones desde consola

- En Linux disponemos de múltiples herramientas:
  - ``fdisk``: Un gestor de particiones de consola presente en casi todas las distribuciones Linux
  - ``cfdisk``: Un gestor de particiones de consola que incorpora las funcionalidades de fdisk pero con una interfaz que facilita
  - ``parted`` y ``Gparted``: Un gestor de particiones de consola que también dispone de un gestor gráfico y que viene preinstalado en múltiples distribuciones


Crear partición y dar formato
=============================

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

La herramienta fdisk permite listar y modificar la tabla de particiones de un disco.

Para listar todos los discos detectados y sus particiones se ejecuta: ``fdisk -l``

Para listar la tabla de particiones del disco ``/dev/sda`` se ejecuta: ``fdisk -l /dev/sda``

Para ejecutar el comando hay que pasarle como argumento el disco sobre el que se desea trabajar (/dev/sda, /dev/sdb, etc.). El comando a ejecutar es: ``fdisk <disco>``

Funciona como un intérprete de comandos, en modo interactivo, en el que los subcomandos más importantes son:

* ``m (man)``: imprime la ayuda.

* ``p (print)``: imprime la tabla de particiones del dispositivo.

* ``d (delete)``: eliminar partición.

* ``n (new)``: crea una nueva partición.

* ``q (quit)``: salir sin guardar los cambios.

* ``w (write)``: escribir los cambios y salir.

Para crear una nueva partición se elige la letra "n".
Se le da formato a la partición con el comando ``mkfs (make filesystem)``. Actualmente, en GNU/Linux existe un programa separado por cada tipo de sistema de ficheros: ``mkfs.ext2, mkfs.ext3, mkfs.ext4, mkfs.ntfs, mkfs.xfs, mkfs.msdos, mkfs.fat, mkfs.vfat`` (es un alias de mkfs.fat), etc. De esta forma mkfs es solamente un front-end que ejecuta el programa apropiado dependiendo del tipo de sistema de ficheros especificado; lo cual haremos con la opción ``-t`` de mkfs.

En primer lugar, vamos a ver qué tipos de formatos podemos dar con mkfs. Para ello, escribimos en una consola mkfs y pulsamos tabulador, para que nos muestre las opciones disponibles:

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


El sistema mantiene actualizada una lista de sistemas de archivos montados a través del archivo ``/proc/self/mounts`` (se actualiza al montar y desmontar sistemas de archivos)

Se pueden listar todas las particiones montadas ejecutando el comando mount

Para "desmontar" la partición, se deshace el vínculo entre la partición y la carpeta en la que se accede a ella. Se puede utilizar el nombre de la partición o el nombre de la carpeta con el comando: ``umount /dev/sdXY`` o bien ``umount /mnt``

Es importante desmontar una partición, especialmente si se han escrito datos. En el caso de los dispositivos extraíbles, si se saca el dispositivo antes de desmontar la partición es bastante probable que se pierdan datos. Al desmontar el dispositivo, se volcarán todas las cachés de escritura al dispositivo.

Las particiones que se monten con el comando ``mount`` no permanecerán después de reiniciar el sistema. Si se quiere montar una partición de forma permanente habrá que añadir una entrada en el fichero /etc/fstab. Durante el arranque del equipo se leen las entradas de este fichero y se montan automáticamente para que estén accesibles a los usuarios.
