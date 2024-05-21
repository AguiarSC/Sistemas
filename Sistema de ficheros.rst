SISTEMAS DE ARCHIVOS
======================

¿Qué es un sistema de archivos?
-------------------------------

Un sistema de archivos es un método de almacenamiento y organización por segmentación de ficheros para facilitar su búsqueda y acceso,los sistemas operativos tienen su propio sistema de archivos, los cuales suelen ser representados de forma textual o gráfica.
En un sistema de archivos hay dos tipos fundamentales de objetos: los directorios(carpetas) y los archivos. 

Archivos:
---------

Las reglas para nombrar los archivos varían dependiendo del sistema, algunos son case-sensitive, otros utilizan un n.º máximo de caracteres, etc.

Atributos:
    - S: System. Atributo del sistema (uso del sistema operativo, uso interno)

    - H: Hidden. Atributo de archivo oculto

    - R: Read. Atributo de sólo lectura

    - A: Atribute. Atributo de archivo, listo para archivar históricamente (se cambia cuand se modifica el archivo, es útil para determinar cuales se modificaron después de la última copia de seguridad).

    - Fecha, hora, tamaño.


En Linux se utilizan también atributos para indicar la pertenencia del archivo, permisos del propietario sobre el archivo, así como el tipo de archivo que es.
Windows permite indicar si el archivo estará cifrado o comprimido.

Directorios:
------------

Son una división lógica de almacenamiento de archivos u otros subdirectorios.

En todo sistema de archivos hay un directorio especial llamado raíz que es el directorio que contiene todos los demás directorios y archivos. Se le suele identificar con una barra inclinada.

En Windows, las rutas de acceso se separan con el carácter ``\`` y en Linux con ``/``. 

Sistema de archivo de Linux.
------------------------------

+-----------------------------------------+----------------------------+
| Modificador                             | Significado                |
+=========================================+============================+
| ``/ : raíz``                            | Directorio principal.      |
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
| ``/root``                               | Carpeta del superusuario.  |
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


Implementación:
--------------------

El aspecto clave de la implementación del almacenamiento de archivos es el registro de los bloques asociados a cada archivo. Un bloque está compuesto por un determinado nº de sectores que se asocian a un único archivo.

Tecnicas de asignacion de bloques a archivos:
---------------------------------------------

- Asignación contigua o adyacente: Se almacenan los archivos mediante bloques adyacentes en el disco. Ventaja: fácil de implementar. Inconveniente: es necesario conocer a priori el número de bloques que ocupará el fichero y genera fragmentación, lo que produce, pérdida de espacio. 

- Asignación en forma de lista enlazada: El directorio contiene la dirección del primer bloque y cada bloque la dirección del siguiente bloque.

- Asignación mediante una lista enlazada y un índice: Se crea una tabla con un registro por cada uno de los bloques del disco, en cada registro se indica si dicho bloque está libre o cuál es la dirección del siguiente bloque. Así, en el directorio se asocia con el nombre del archivo el número de bloque en el que comienza dicho archivo. Utilizada en FAT 16 y FAT 32.

- Basado en inodos:se asocia a cada archivo una pequeña tabla, llamada inodo, quecontiene los atributos y direcciones en disco de los bloques del archivo(Linux). 

        -Propiedades:
            - id,nº de inodo,longitud, id de usuario y grupo,modo de acceso,nº de enlaces y marca de tiempo.

            - Estructura de punteros, para direccionar hacia los bloques de datos del archivo.
    
            +-----------------------------------------+----------------------------------------------------+
            | ``puntero indireccion simple``          | Apunta a un bloque de punteros, los cuales apuntan |
            |                                         | a bloques de datos del archivo.                    |
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

Las GUIs en Linux se cargan gracias al X-Window System que define unos protocolos de comunicación y visualización de ventanas. Es propio de UNIX, libre y de código abierto. El servidor X controla los dispositivos periféricos como el teclado, el ratón, y la pantalla. Se puede iniciar mediante un comando aunque normalmente se ejecuta al arrancar el sistema. 

Escritorio:

    - GNOME: Forma parte del proyecto GNU, tiene licencia GPL y es el escritorio por defecto de Ubuntu.
    - KDE : Es un entorno para GNU/Linux y otros sistemas derivados de UNIX. La versión de Ubuntu que utiliza KDE se denomina Kubuntu. 

Tipos de usuario y de permisos:

    - Propietario (owner): creador del archivo

    - Grupo (group): conjunto de usuarios

    - Resto de usuarios (others): usuarios que no pertenecen a un grupo ni son propietarios


    - Lectura (r, read): ver e imprimir archivos; se pueden ver todos los elementos del directorio.

    - Escritura (w, write): cambiar o eliminar archivos o directorios.

    - Ejecución (x, execute): el fichero puede ser ejecutado. 

Establecer y cambiar permisos:
------------------------------
En Linux cada archivo queda identificado por diez caracteres.

El primer carácter empezando por la izquierda indica el tipo de archivo. 

        - Normal (-), directorio (d), enlace simbólico (l), entrada y salida (c,b,s,p).

Los nueve caracteres siguientes organizados en conjuntos de tres indican los permisos para cada categoría de usuarios. Las categorías de usuarios (empezando por la izquierda) son propietario, grupo y resto de usuarios. 

La asignación de permisos en esos 3 catacteres que indican la categoria de los usuarios podria ser de dos maneras:
   
Por octal
        
        - El valor de cada uno de esos tres dígitos se calcula teniendo en cuenta el orden de permisos (rwx). Si se asigna permiso se utilizará un 1, si no se asigna se utilizará un 0. A continuación se hará la conversión de binario a octal.

Por letras que indican:

        - quien: u (usuarios), g (grupo), o (otros), a (todos)
        - operación: + (añadir) y - (eliminar), = (asignar).
        - permisos: r (lectura), w (escritura), x (ejecución) 

Permisos especiales 
-------------------

- Sticky bit(t)

    Significa que tan solo los respectivos dueños de los archivos que haya en el directorio y el superusuario pueden borrarlos.

- SUID(s)

    Cuando a un ejecutable binario se le asigna el atributo setuid, usuarios normales del sistema pueden ejecutar ese archivo y obtener privilegios del superusuario

- SGID(s)

    Es lo mismo que en el SUID, peroa nivel de grupo.Tiene privilegios de grupo en un directorio colaborativo.

Si cualquiera de estos permisos salen escritos en mayúsculas significa que para que sea efectivo el permiso debe tener permisos de ejecución.

Permisos de directorio:
-----------------------

• En un directorio con permiso de escritura se puede:

    - Añadir y borrar archivos, aunque sobre estos no se tenga permiso de escritura.

    - Añadir directorios y borrarlos si los permisos de estos lo permiten.

    - Modificar archivos siempre que los permisos de estos lo permitan.

• En un directorio sin permiso de escritura:

    - No se puede añadir ni borrar archivos ni directorios.

    - Se puede modificar el contenido de los archivos siempre que se tenga permiso de escritura sobre ellos.

• En un directorio sin permiso de lectura:

    - No se puede ver lo que hay dentro.

• En un directorio sin permiso de ejecución

    - No se puede hacer nada.

Enlaces:
-----------

Simbólicos (o blandos) 
----------------------

- Usar rutas absolutas al especificar el origen.

- Puede crearse un enlace simbólico aunque el archivo que representa no exista.

- Si se borra el enlace no pasa nada, el archivo original sigue permanece intacto.

- Si se borra el archivo original, el enlace no es accesible.

- Cuando se utilizan más de dos argumentos, el último debe ser un directorio existente, en el que se crearán los enlaces simbólicos a los argumentos anteriores con el nombre básico de los mismos.

- Si se copia un enlace, se copia el contenido del archivo, pero no el enlace en sí.

- Los enlaces simbólicos, aparecerán en los listados con el carácter “l” en la columna de los permisos y con un puntero en la columna del nombre de fichero.

- A los enlaces simbólicos se le asignan automáticamente todos los permisos. 

Duros (o fuertes) 
-----------------

- Los enlaces duros no pueden hacerse con directorios.

- Si se borra alguno de los enlaces, el archivo sigue existiendo mientras exista uno de los enlaces, ya que todos están apuntando al mismo bloque de datos,es decir, al mismo i-nodo.

- Para saber si un archivo tiene enlaces físicos, se mira en la columna Links del comando ls en formato largo, para comprobar que el número que aparece es más grande que 1.

- Cuando se utilizan más de dos argumentos, el último debe ser un directorio existente, en el que se crearán los enlaces a los argumentos anteriores con el nombre básico de los mismos.

- No aparecen marcados de ningún modo especial.


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

