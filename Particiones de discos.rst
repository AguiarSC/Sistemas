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

