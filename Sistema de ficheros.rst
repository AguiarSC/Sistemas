SISTEMAS DE ARCHIVOS
======================

¿Qué es un sistema de archivos?
-------------------------------

Un sistema de archivos es un ``método de almacenamiento y organización por segmentación de ficheros para facilitar su búsqueda y acceso``. Los sistemas operativos tienen su propio sistema de archivos, los cuales suelen ser representados de forma textual o gráfica.
En un sistema de archivos hay dos tipos fundamentales de objetos: los ``directorios`` y los ``archivos``. 

Archivos:
---------

Las reglas para nombrar los archivos varían dependiendo del sistema, algunos son case-sensitive, otros utilizan un n.º máximo de caracteres, etc.

Atributos:
    - ``S``: System. Uso interno del SO.

    - ``H``: Hidden. No visible en la exploración.

    - ``R``: Read. El archivo solo puede leerse.

    - ``A``: Atribute. Listo para ser archivado. Utilidad para ``backups`` al actualizarse al editarlo. 

    - ``Fecha``, ``hora``, ``tamaño``, ``pertenencia del archivo``, ``permisos del propietario``, ``tipo de archivo``, etc.

``Windows`` permite indicar si el archivo estará ``cifrado`` o ``comprimido``.

Directorios:
------------

Son una ``división lógica de almacenamiento de archivos u otros subdirectorios``.

En todo sistema de archivos hay un directorio especial llamado ``raíz`` que es el directorio que contiene todos los demás directorios y archivos. Se le suele identificar con una barra inclinada.

En Windows, las rutas de acceso se separan con el carácter ``\`` y en Linux con ``/``. 

Sistema de archivo de Linux.
------------------------------

+-----------------------------------------+----------------------------+
| Modificador                             | Significado                |
+=========================================+============================+
| ``/``                                   | Directorio principal.      |
+-----------------------------------------+----------------------------+
| ``/bin``                                | Son instrucciones          |
|                                         | fundamentales que se       |
|                                         | ejecutan al iniciar el     |
|                                         | sistema para que los user  |
|                                         | normales puedan usar       |
|                                         | ciertos programas.         | 
+-----------------------------------------+----------------------------+
| ``/boot``                               | Archivos de arranque,      |
|                                         | utilizados por el gestor   |
|                                         | de arranque.               |
+-----------------------------------------+----------------------------+
| ``/cdrom``                              | Lugar donde se sitúa la    |
|                                         | unidad de CD-ROM.          |
+-----------------------------------------+----------------------------+
| ``/dev``                                | Archivos de dispositivos a |
|                                         | los que se puede acceder.  |
+-----------------------------------------+----------------------------+
| ``/etc``                                | Archivos de configuración y|
|                                         | administración del sistema.|
+-----------------------------------------+----------------------------+
| ``/home``                               | Contiene los directorios de|
|                                         | trabajo de los usuarios.   |
+-----------------------------------------+----------------------------+
| ``/media``                              | Guarda las ubicaciones     |
|                                         | donde se conectan          |
|                                         | dispositivos externos.     |
+-----------------------------------------+----------------------------+
| ``/mnt``                                | Punto de montaje temporal  |
|                                         | donde se montan particiones|
|                                         | los dispositivos de        |
|                                         | almacenamiento...          |
+-----------------------------------------+----------------------------+
| ``/lib``                                | Librerías compartidas      |
|                                         | necesarias para programas. |
+-----------------------------------------+----------------------------+
| ``/opt``                                | Datos de paquetes software |
|                                         | adicionales.               |
+-----------------------------------------+----------------------------+
| ``/proc``                               | Información sobre procesos |
|                                         | del sistema que se están   |
|                                         | ejecutando.                |
+-----------------------------------------+----------------------------+
| ``/root``                               | Carpeta del usuario root.  |
+-----------------------------------------+----------------------------+
| ``/sbin``                               | Programas para configurar  |
|                                         | el sistema.                |
+-----------------------------------------+----------------------------+
| ``/sys``                                | Dispositivos de conexión   |
|                                         | en caliente.               |
+-----------------------------------------+----------------------------+
| ``/tmp``                                | Ficheros temporales,suele   |
|                                         | ser un enlace simbólico.   |
+-----------------------------------------+----------------------------+
| ``/usr``                                | Donde se instalan las apps |
|                                         | de cada usuario.           |
+-----------------------------------------+----------------------------+
| ``/var``                                | Contiene datos que varían  |
|                                         | de sistema que se modifican|
|                                         | al ser ejecutado           |
+-----------------------------------------+----------------------------+

Sistema de archivo de Windows.
------------------------------

+-----------------------------------------+---------------------------------------------+
| Modificador                             | Significado                                 |
+=========================================+=============================================+
| ``Archivos de programa``                | Donde se instalan los nuevos programas      |
+-----------------------------------------+---------------------------------------------+
| ``Usuarios``                            | Contiene las carpetas de los usuarios       |
+-----------------------------------------+---------------------------------------------+
| ``Windows``                             | Contiene carpetas y archivos necesarios     |
|                                         | para que funcione el sistema                |
+-----------------------------------------+---------------------------------------------+


Registro de Bloques
-------------------
El almacenamiento de archivos se basa en registrar los bloques de datos asociados a cada archivo. Un ``bloque`` es un conjunto de sectores del disco asignados a un solo archivo.

Tecnicas de asignación de bloques
---------------------------------

- ``Asignación contigua``: se almacenan en bloques contiguos en el disco. Es fácil de implementar, pero se debe conocer de antemano el número de bloques que ocupará el archivo. Provoca fragmentación externa.

- ``Asignación en lista enlazada``: el directorio contiene la dirección del primer bloque y cada bloque la dirección del siguiente bloque. No requiere conocer el tamaño del archivo por adelantado, pero es más lento.

- ``Asignación mediante lista enlazada e índice``: Se utiliza una tabla (FAT) con un registro para cada bloque del disco. Cada registro indica si el bloque está libre o la dirección del siguiente bloque. El directorio asocia el nombre del archivo con el número del bloque inicial. Eficiente en términos de espacio (si son pequeños o medianos). Ampliamente utilizado en sistemas FAT16 y FAT32. 

- ``Basado en inodos``: cada archivo tiene un inodo que contiene sus atributos y las direcciones en el disco de sus bloques de datos. Sus propiedades son: ``id``, ``longitud``, ``id de usuario`` y ``grupo``, ``modo de acceso``, ``n.º de enlaces`` y ``marca de tiempo``. Presenta una estructura de ``punteros`` (variable que apunta a una ubicación en la memoria donde esté el valor de otra variable), para direccionar hacia los bloques de datos del archivo.
    
            +-----------------------------------------+----------------------------------------------------+
            | ``puntero indireccion simple``          | Apunta a un bloque de punteros, los cuales, cada   |
            |                                         | uno, apuntan a bloques de datos del archivo.       |
            +-----------------------------------------+----------------------------------------------------+
            | ``puntero indireccion doble``           | Apunta a un bloque de punteros, los cuales apuntan |
            |                                         | a otros bloques de punteros, estos últimos apuntan |
            |                                         | a bloques de datos del archivo.                    |
            +-----------------------------------------+----------------------------------------------------+
            | ``puntero indireccion triple``          | Apunta a un bloque de punteros, los cuales apuntan |
            |                                         | a otros bloques de punteros, que apuntan a otros   |
            |                                         | bloques de punteros que apuntan a bloques de datos |
            |                                         | del archivo.                                       |
            +-----------------------------------------+----------------------------------------------------+

Entorno gráfico (Linux):
--------------------------

Las ``GUI`` en Linux se cargan gracias al ``X-Window System`` que define unos protocolos de comunicación y visualización de ventanas.

- ``GNOME``: escritorio por defecto de Ubuntu.
- ``KDE`` : entorno para GNU/Linux y otros sistemas derivados de UNIX. La versión de Ubuntu se denomina Kubuntu. 


Tipos de usuario y de permisos
------------------------------

    - ``Propietario`` (owner): creador del archivo

    - ``Grupo`` (group): conjunto de usuarios

    - ``Otros`` (others): usuarios que no pertenecen a un grupo ni son propietarios


    - ``Lectura`` (r, read): ver e imprimir archivos; se pueden ver todos los elementos del directorio.

    - ``Escritura`` (w, write): cambiar o eliminar archivos o directorios.

    - ``Ejecución`` (x, Xecute): el fichero puede ser ejecutado. 


Establecer y cambiar permisos
-----------------------------

En Linux, ``cada archivo está identificado por 10 caracteres``.

El ``1`` indica el ``tipo de archivo``: normal (`-`), directorio (`d`), enlace simbólico (`l`), entrada y salida (`c`, `b`, `s`, `p`).

``2 - 10``, organizados en ``conjuntos de tres``, indican los ``permisos para cada categoría de usuarios``(propietario, grupo y otros).

La ``asignación de permisos en esos tres caracteres`` que indican la categoría de los usuarios puede hacerse de ``dos maneras``:

Por octal
---------

El ``valor de cada uno de esos tres dígitos`` se calcula teniendo en cuenta el orden de permisos (``rwx``). Si se asigna permiso se utilizará un ``1``, si no se asigna se utilizará un ``0``.

Para convertir permisos en formato ``rwxr-x--x`` a ``octal``, asigna valores numéricos: ``r = 4``, ``w = 2``, ``x = 1``, ``- = 0``. 
Luego, ``agrupa en tríos de permisos y suma los valores``. Por ejemplo, ``rwx = 7``, ``r-x = 5``, ``--x = 1``. Entonces, ``rwxr-x--x`` se convierte en ``751`` en octal.

Por letras
----------

  - quién: ``u`` (usuarios), ``g`` (grupo), ``o`` (otros), ``a`` (todos)
  - operación: ``+`` (añadir), ``-`` (eliminar), ``=`` (asignar)
  - permisos: ``r`` (lectura), ``w`` (escritura), ``x`` (ejecución)

    .. code-block:: sh
    
        chmod u+x archivo1 añade permiso de ejecución al usuario propietario.
        chmod go-w archivo2 quita permiso de escritura al grupo y otros.
        chmod o=r archivo3 establece permisos de solo lectura para otros.
    ..

Permisos especiales
===================

``Sticky bit (t)``

Solo el ``propietario del archivo``, el ``propietario del directorio`` y el ``root`` pueden ``eliminar o mover archivos`` dentro de ese directorio. 


``SUID (s)``

Cuando a un ejecutable binario se le asigna el atributo ``setuid``, los usuarios normales del sistema pueden ejecutar ese archivo y obtener ``privilegios del root``.


``SGID (s)``

Lo mismo que el SUID, pero a nivel de grupo. Tiene ``privilegios de grupo`` en un directorio colaborativo.

``Si cualquiera de estos permisos se escribe en mayúsculas, significa que para que el permiso sea efectivo, debe tener permisos de ejecución.``

Permisos de directorio
======================

- ``Con permiso de escritura``
  - Se pueden añadir y borrar archivos, aunque no se tenga permiso de escritura sobre ellos.
  - Se pueden añadir y borrar directorios si los permisos lo permiten.
  - Se pueden modificar archivos siempre que los permisos lo permitan.

- ``Sin permiso de escritura``
  - No se puede añadir ni borrar archivos ni directorios.
  - Se puede modificar el contenido de los archivos si se tiene permiso de escritura sobre ellos.

- ``Sin permiso de lectura``
  - No se puede ver el contenido del directorio.

- ``Sin permiso de ejecución``
  - No se puede acceder al directorio ni realizar ninguna acción en él.


Enlaces
=======

Enlaces Simbólicos (o blandos)
--------------------------------

- Son referencias a archivos o directorios.
- Pueden apuntar a cualquier ubicación con rutas relativas o absolutas.
- Pueden cruzar sistemas de archivos o particiones.

Enlaces Duros (o fuertes)
--------------------------

- Son referencias a archivos o directorios.
- Pueden apuntar a cualquier ubicación con rutas relativas o absolutas.
- Pueden cruzar sistemas de archivos o particiones.


Listados:
------------

.. code-block:: bash

    drwxr-xr-x 2 usuario grupo 4096 May 13 2024 directorio
    -rw-r--r-- 1 usuario grupo   12 May 13 2024 archivo_normal
    brw-r----- 1 usuario grupo    0 May 13 2024 bloque
    crw-rw---- 1 usuario grupo    0 May 13 2024 caracter
    lrwxrwxrwx 1 usuario grupo    7 May 13 2024 enlace_simbolico -> archivo
    prw-r----- 1 usuario grupo    0 May 13 2024 tuberia
    srwxrwxrwx 1 usuario grupo    0 May 13 2024 socket


* ``Tipo de archivo``: La primera columna indica el tipo de archivo o entrada. 

    * ``d``: Indica un directorio.

    * ``-``: Representa un archivo normal o usual, que puede ser creado con programas como vi, cp, touch, etc.

    * ``b``: Es un archivo tipo bloque, utilizado para entrada/salida en bloques de datos.

    * ``c``: Se refiere a un archivo tipo carácter, utilizado para entrada/salida byte a byte.

    * ``l``: Representa un enlace simbólico, que apunta a otro fichero.

    * ``p``: Indica pipes o tuberías, que permiten la comunicación entre procesos y se crean con mknod.

    * ``s``: Representa sockets, que se utilizan para la comunicación entre procesos en la red. En Linux, todos estos elementos son considerados archivos, pero los directorios son tratados como un tipo de archivo distinto de los archivos normales.

    * Además, los siguientes caracteres (de tres en tres) representan los ``permisos del propietario``, ``del grupo`` y de ``otros usuarios`` respectivamente: ``r: lectura``, ``w: escritura``, ``x: ejecución``.

* ``Links``: Esta segunda columna indica si el objeto es un archivo y el número de enlaces completos o duros. Si es un archivo, muestra el número de enlaces duros que tiene. Si es un directorio, el número de objetos que cuelgan de él más 2, que incluyen el propio directorio y el directorio padre.

* ``Información básica``: Las columnas restantes contienen información básica sobre el archivo o directorio, como el nombre de usuario propietario, el grupo al que pertenece, la fecha y hora de la última modificación y el tamaño del archivo en bytes.

