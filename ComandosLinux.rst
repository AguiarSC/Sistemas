Comandos Linux :
=================
¿Como se interpretan los comandos?
-----------------------------------
Los comandos se interpretan a traves de un interprete de comandos o shell.El shell actúa de interface entre el usuario y el núcleo de Linux.El cual te muestra una indicacion para anunciar que espera una orden del usuario (prompt).

El intérprete de comandos más utilizado actualmente es el bash  que tiene las siguientes caracteristicas.

    - Distingue mayúsculas y minúsculas.
    - Almacena un historial de los últimos comandos introducidos por el usuario.
    - El comando exit cierra una sesión en modo texto.
    - Los intérpretes de comandos permiten pasarles parámetros a los comandos:
                • Los parámetros se introducen después del comando con el símbolo - (guion).
                • Se pueden combinar distintos parámetros. Ej: ls -laR.
                • No importa el orden en el que se introduzcan los distintos parámetros del comando.

Igual que en otros sistemas operativos, cuando hacemos referencia a los elementos del sistema de ficheros podemos hacerlo de dos formas:
    • Relativa: indicando la ruta a partir del directorio de trabajo
    • Absoluta: indicando una ruta completa al elemento a partir del directorio raíz.

Comandos (Linux):
------------------


+------------------------------------+-------------------------------------------------------------+
| Comando                            | Descripción                                                 |
+====================================+=============================================================+
| ``uname``                          | ``m`` arquitectura ``r`` version Kernel                     |
| ``[-anmr]``                        | ``-a`` nombre sistema y ordenador                           |
|                                    | ``-n`` nombre del ordenador                                 |
+------------------------------------+-------------------------------------------------------------+
| ``logname whoami``                 | Ususario actual                                             |
+------------------------------------+-------------------------------------------------------------+
| ``lsb_release -a``                 | Distribución de Linux                                       |
+------------------------------------+-------------------------------------------------------------+
| ``pstree``                         | Mostrar la estructura arborescente de procesos             |
+------------------------------------+-------------------------------------------------------------+
| ``who``                            | Datos de usuario                                            |
+------------------------------------+-------------------------------------------------------------+
| ``id [-ug] [usuario]``             | Identificación de un usuario                                |
|                                    | ``-i`` usuario ``-g`` grupo                                 |
+------------------------------------+-------------------------------------------------------------+
| ``ls``                             | Listar archivos y directorios                               |
|                                    |                                                             |
|                                    | ``-l`` Lista informacion(permisos usuario grupo...)         |
|                                    |                                                             |
|                                    | ``-t`` Ordenado por la fecha de última modificación         |
|                                    |                                                             |
|                                    | ``-r`` Muestra los archivos más recientes al final          |
|                                    |                                                             |
|                                    | ``-m`` Muestra los archivos en una línea y separados por comas.|
|                                    |                                                             |
|                                    | ``-a`` muestra los archivos ocultos.                        |
|                                    |                                                             |
|                                    | ``-R`` Primero los archivos del directorio en curso,luego sus subdirectorios|
|                                    |                                                             |
|                                    | ``-F`` Visualiza un * junto a los ejecutables, una / junto a|
|                                    | los directorios y @ junto a los enlaces simbólicos.         |
|                                    |                                                             |
|                                    | ``-d`` Proporciona información del directorio NO su contenido|
+------------------------------------+-------------------------------------------------------------+
| ``cal``                            | Calendario                                                  |
+------------------------------------+-------------------------------------------------------------+
| ``clear``                          | Limpiar pantalla                                            |
+------------------------------------+-------------------------------------------------------------+
| ``pwd``                            | Directorio actual                                           |
+------------------------------------+-------------------------------------------------------------+
| ``file nomfich``                   | Tipo de archivo                                             |
+------------------------------------+-------------------------------------------------------------+
| ``man, info``                      | Manual completo sobre un comando/info muy detallada         |
|                                    |                                                             |
| ``whatis``                         | Información reducida del comando                            |
| ``apropos``                        |                                                             |
|                                    |                                                             |
| ``--help,-h``                      | Ayuda basica sobre un comando                               |
+------------------------------------+-------------------------------------------------------------+
| ``cd``                             | Cambiar de directorio                                       |
|                                    |                                                             |
| ``cd -``                           | directorio anterior                                         |
|                                    |                                                             |
| ``Sin directorio``                 | directorio personal del usuario.HOME                        |
|                                    |                                                             |
| ``/directorio``                    | Accede a /directorio (ruta absoluta)                        |
|                                    |                                                             |
| ``directorio``                     | Accede a una carpeta contenida en el directorio actual      |
|                                    |                                                             |
| ``cd ..``                          | Se accede al directorio padre                               |
+------------------------------------+-------------------------------------------------------------+
| ``sudo nano nombrearchivo.txt``    | Crear un documento y modificarlo                            |
|                                    |                                                             |
| ``vi, cat >>``                     |                                                             |
+------------------------------------+-------------------------------------------------------------+
| ``touch ,:>``                      | Crear un documento en blanco                                |
|                                    |                                                             |
| ``cat >``                          |                                                             |
+------------------------------------+-------------------------------------------------------------+
| ``cat, more``                      | Visualizar contenido en fichero/more= de forma paginada     |
|                                    |                                                             |
| ``less, head -n``                  | permite moverse por el archivo con los cursores/            |
|                                    | para visualizar las N primeras líneas                       |
|                                    |                                                             |
| ``tail``                           | para visualizar las N últimas líneas                        |
+------------------------------------+-------------------------------------------------------------+
| ``cp [opciones] origen destino``   | Copiar archivos y directorios                               |
|                                    |                                                             |
|                                    | ``-f`` Sobreescribe un fichero con el mismo nombre          |
|                                    |                                                             |
|                                    | ``-p`` Se incluyen los atributos de origen en destino       |
|                                    |                                                             |
|                                    | ``-i`` Pregunta antes de sobreescribir                      |
|                                    |                                                             |
|                                    | ``-u`` Sobreescribe cuando el fichero a copiar es más actual|
|                                    |                                                             |
|                                    | ``-v`` Indica los archivos que se van copiando              |
|                                    |                                                             |
|                                    | ``-R`` Copia de forma recursiva todo lo que cuelga del directorio1|
+------------------------------------+-------------------------------------------------------------+
| ``mv nombre1 nombre2``             | 1(renombrar)2(mover)                                        |
|                                    |                                                             |
| ``mv [opciones] origen destino``   | Son las mismas opciones que el de copiar menos ``-R y -p``  |
+------------------------------------+-------------------------------------------------------------+
| ``Lpr``                            | Envía un trabajo a la impresora                             |
|                                    |                                                             |
| ``lpq``                            | Muestra los trabajos pendientes de la impresora             |
|                                    |                                                             |
| ``Lprm``                           | Elimina un trabajo de la cola de la impresora               |
+------------------------------------+-------------------------------------------------------------+
| ``alias``                          | Alias para ejecutar comandos                                |
+------------------------------------+-------------------------------------------------------------+
| ``unalias``                        | Borrar alias creado                                         |
+------------------------------------+-------------------------------------------------------------+
| ``chmod``                          | Establecer y cambiar permisos en ficheros y/o directorios.  |
|                                    |                                                             |
+------------------------------------+-------------------------------------------------------------+
| ``umask``                          | muestra la máscara establecida                              |
|                                    | si añades nnn es el valor octal restado del valor por omisión |
+------------------------------------+-------------------------------------------------------------+
| ``wc [-lwcL]``                     | Cuenteo de ficheros                                         |
|                                    | (de lineas,palabras,nº bytes                                |
|                                    | y longitud línea más larga)                                 |
+------------------------------------+-------------------------------------------------------------+
| ``mkdir``                          | Crear directorios                                           |
|                                    |                                                             |
| ``mkdir -opcion``                  | ``-p`` Crear estructura de directorios                      |
|                                    |                                                             |
|                                    | ``-v`` Muestra el nombre del directorio creado              |
|                                    |                                                             |
|                                    | ``-m`` Permisos.                                            |
+------------------------------------+-------------------------------------------------------------+
| ``rm [opciones] fichero``          | Borrar archivos (ficheros)/(directorios)                    |
|                                    |                                                             |
| ``rm - r o -R``                    |                                                             |
|                                    |                                                             |
|                                    | ``-f`` Elimina cualquier aviso de confirmación              |
|                                    |                                                             |
|                                    | ``-i`` Pregunta antes de cada borrado                       |
|                                    |                                                             |
|                                    | ``-v`` Muestra el nombre de cada fichero antes de borrarlo  |
+------------------------------------+-------------------------------------------------------------+
| ``chown``                          | Cambiar propietario fich/direct                             |
|                                    |                                                             |
|                                    |chown [-R] propietario[:grupo] archivo1 | directorio1        |
|                                    |[archivo2 |directorio2 ..]                                   |
|                                    |                                                             |
|                                    | propietario nombre del usuario que sera propietario         |
|                                    |                                                             |
|                                    | :grupo nombre del nuevo grupo                               |
|                                    |                                                             |
|                                    | archivo1/directorio1 Nombre de los archivos/directorios     |
|                                    | a los que se les cambia el propietario.                     |
|                                    |                                                             |
|                                    | -R se utiliza con directorios, y lo que hace es cambiar el  |
|                                    | propietario y/o grupo a dicho directorio y a todo lo que él contiene|
+------------------------------------+-------------------------------------------------------------+
| ``chgrp``                          | Cambiar grupo fichero directorio                            |
|                                    |                                                             |
|                                    |chgrp [-R] grupo archivo1/directorio1 archivo2/directorio2...|
|                                    |                                                             |
|                                    | igual que arriba solo que en vez de cambiar propietarios son grupos|
+------------------------------------+-------------------------------------------------------------+
| ``diff``                           | Compara 2 ficheros línea a línea                            |
+------------------------------------+-------------------------------------------------------------+
| ``cmp``                            | Compara 2 ficheros byte a byte                              |
+------------------------------------+-------------------------------------------------------------+
| ``tac``                            | Muestra contenido de un fichero                             |
|                                    | empezando por el final                                      |
|                                    | (al revés que cat)                                          |
+------------------------------------+-------------------------------------------------------------+
| ``tree``                           | Muestra el árbol de directorios                             |
+------------------------------------+-------------------------------------------------------------+
| ``ln y ln -s``                     | Crear enlaces fuertes/simbolicos                            |
+------------------------------------+-------------------------------------------------------------+
| ``tar, zip/unzip``                 | Comprimir y descomprimir                                    |
|                                    |                                                             |
| ``tar -tf``                        | /lista sin descomprimir                                     |
|                                    |                                                             |
| ``-cvzfxj``                        |``c``comprime``f``nombre de fichero                          |
|                                    |                                                             |
|                                    |``v``muestra proceso por pantalla                            |
|                                    |                                                             |
|                                    |``f``archivo                                                 |
|                                    |                                                             |
|                                    |``d``descomprimir                                            |
|                                    |                                                             |
|                                    |``r``De forma recursiva                                      |
|                                    |                                                             |
|                                    |``j``representa compresión bz2                               |
|                                    |                                                             |
|                                    |``x``Extraer                                                 |
|                                    |                                                             |
|                                    |``z`` compresión gzip                                        |
+------------------------------------+-------------------------------------------------------------+
| ``uniq``                           | Suprime o informa de líneas                                 |
|                                    | duplicadas consecutivas                                     |
+------------------------------------+-------------------------------------------------------------+
| ``tee``                            | Redirige la salida estándar de                              |
|                                    | un comando a un archivo, muestra                            |
|                                    | la salida estandar en terminal                              |
+------------------------------------+-------------------------------------------------------------+
| ``sort``                           | Ordena las líneas de un fichero                             |
|                                    | o indica si está ordenado                                   |
+------------------------------------+-------------------------------------------------------------+
| ``find``                           | Busca ficheros que coincidan                                |
|                                    | empezando por el final                                      |
|                                    | (al revés que cat)                                          |
+------------------------------------+-------------------------------------------------------------+
| ``cut``                            | Elimina secciones de cada línea                             |
|                                    | de uno o varios ficheros                                    |
+------------------------------------+-------------------------------------------------------------+
| ``awk``                            | Procesar texto y mostrar líneas                             |
|                                    | con el patrón por el árbol                                  |
|                                    | de directorios                                              |
+------------------------------------+-------------------------------------------------------------+
| ``sed``                            | Para buscar, reemplazar un texto                            |
|                                    | palabras,patrones,etc                                       |
+------------------------------------+-------------------------------------------------------------+
| ``tr``                             | Copia la entrada estándar                                   |
|                                    | en la salida estándar                                       |
|                                    | sustituyendo o borrando los                                 |
|                                    | caracteres seleccionados                                    |
+------------------------------------+-------------------------------------------------------------+
| ``grep``                           | Busca coincidencias del patrón                              |
|                                    | en ficheros                                                 |
+------------------------------------+-------------------------------------------------------------+
| ``date  [+formato]``               | Fecha y hora                                                |
+------------------------------------+-------------------------------------------------------------+
| ``useradd [opciones] login``       |Crear usuario                                                |
|                                    |                                                             |
|                                    |``c`` crea un comentario para un usuario                     |
|                                    |                                                             |
|                                    |``d`` establece un directorio como directorio de trabajo     |
|                                    |                                                             |
|                                    |``p`` establece la contraseña del usuario                    |
|                                    |                                                             |
|                                    |``g`` asignación al grupo principal                          |
|                                    |                                                             |
|                                    |``G`` lista de grupos secundariosa                           |
|                                    |                                                             |
|                                    |``s`` establece un intérprete de comandos al usuario         |
|                                    |                                                             |
|                                    |``m`` crea el directorio personal                            |
|                                    |                                                             |
|                                    |``e`` fecha en que expira la cuenta del usuario              |
|                                    |                                                             |
|                                    |``f`` Nos permite seleccionar el número de días a partir de la|
|                                    | fecha de expiración de la contraseña para deshabilitar la cuenta|
|                                    |                                                             |
|                                    |``u``permite especificar el identificador de usuario         |
+------------------------------------+-------------------------------------------------------------+
| ``usermod [opciones] login``       |Modificar usuario                                            |
|                                    |                                                             |
|                                    |Mismas opciones que en user add                              |
|                                    |                                                             |
|                                    |``l,–login`` <nuevo nombre>                                  |
|                                    |                                                             |
|                                    |``-L y -U`` Bloquear o desbloquear respectivamente           |
|                                    |                                                             |
|                                    |``-a, –append``añadir usuarios a un grupo                    |
+------------------------------------+-------------------------------------------------------------+
| ``chsh``                           | Cambiar el shell de un usuario                              |
+------------------------------------+-------------------------------------------------------------+
| ``ps [opciones]``                  | Obtiene información de los procesos del sistema             |
|                                    |                                                             |
|                                    | ``aux`` lista y obtiene información de todos los procesos del| 
|                                    | sistema, de todos los usuarios, con información añadida     |
|                                    |                                                             |
|                                    |     ``a``  procesos de todos los usuarios                   |
|                                    |                                                             |
|                                    |     ``u`` información del proceso con más opciones,como la memoria|
|                                    |                                                             |
|                                    |     ``x`` procesos de todas las terminales                  |
|                                    |                                                             |
|                                    | ``f`` muestra los procesos en formato árbol                 |
|                                    |                                                             |
|                                    | ``t`` muestra los procesos generados en la terminal indicada|
|                                    |                                                             |
|                                    | ``U``muestra los procesos generados por el usuario indicado |
|                                    |                                                             |
|                                    | ``l`` muestra campos como prioridad y valor nice que con la |
|                                    | opción aux no aparecían.                                    | 
+------------------------------------+-------------------------------------------------------------+
| ``chfn``                           | Modificar la información de usuario                         |
+------------------------------------+-------------------------------------------------------------+
| ``userdel [-r] login``             | Eliminar un usuario del sistema                             |
+------------------------------------+-------------------------------------------------------------+
|``groupadd [opciones] nombre_grupo``|Crear grupo                                                  |
|                                    |                                                             |
|                                    |``g``  asigna un identificador de grupo al nombre del grupo  |
|                                    |                                                             |
|                                    |``n`` nombre del grupo                                       |
|                                    |                                                             |
|                                    |``p`` establece la contraseña del grupo                      |
+------------------------------------+-------------------------------------------------------------+
|``groupmod [opciones] nombre_grupo``|Modificar grupo                                              |
|                                    |                                                             |
|                                    | ``g`` modificar id de grupo                                 |
|                                    |                                                             |
|                                    |Despues igual que el crear grupo                             |
+------------------------------------+-------------------------------------------------------------+
| ``groupdel nombre_grupo ``         | Eliminar un grupo del sistema                               |
+------------------------------------+-------------------------------------------------------------+
| ``adduser [login_usuario] grupo``  | Añadir usuario a un grupo                                   |
+------------------------------------+-------------------------------------------------------------+
| ``deluser [login_usuario] grupo``  | Eliminar usuario de un grupo                                |
+------------------------------------+-------------------------------------------------------------+
|``openssl passwd [op] pswencriptar``| Permite generar contraseñas hash.                           |
|                                    |                                                             |
|                                    | ``-1`` Algoritmo de encriptación en MD5.                    |
|                                    |                                                             |
|                                    | ``-5`` Algoritmo de encriptación en SHA-256.                |
|                                    |                                                             |
|                                    | ``-6``Algoritmo de encriptación en SHA-512.                 |
+------------------------------------+-------------------------------------------------------------+
|``chage [opciones] [login] ``       | Modificar valores del archivo de configuración /etc/shadow. |
|                                    |                                                             |
|                                    | ``d`` Elimina la contraseña de la cuenta de usuario.        |
|                                    |                                                             |
|                                    | ``E`` Establece la fecha de caducidad de la cuenta          |
|                                    |                                                             |
|                                    | ``i``Establece el número de días de inactividad para que una cuenta se bloquee después de que expire la contraseña.|
|                                    |                                                             |
|                                    | ``l`` Muestra información de caducidad de la contraseña     |
|                                    |                                                             |
|                                    | ``m`` Establece el Nº MIN de días entre cambios de contraseña|
|                                    |                                                             |
|                                    | ``M`` Establece el Nº MAX de días durante los cuales una contraseña es válida|
|                                    |                                                             |
|                                    | ``W``Establece el Nº de días de advertencia previos a que la contraseña caduque.|
+------------------------------------+-------------------------------------------------------------+
| ``passwd [op] nombre_usuario``     | Cambiar contraseña                                          |
|                                    |                                                             |
|                                    | ``-d`` Lista informacion(permisos usuario grupo...)         |
|                                    |                                                             |
|                                    | ``-e`` Expira inmediatamente la contraseña del usuario      |
|                                    |                                                             |
|                                    | ``-i``,``-w``= opciones iguales que las anteriores          |
|                                    |                                                             |
|                                    | ``-l`` Bloquea la contraseña de la cuenta de usuario        |
|                                    |                                                             |
|                                    | ``-u`` Desbloquea la contraseña de la cuenta de usuario     |
|                                    |                                                             |
|                                    | ``-x`` Nº de días que la contraseña es válida               |
+------------------------------------+-------------------------------------------------------------+
| ``du [opciones] [directorio]``     | Muestra el espacio de disco usado por ficheros y subdirectorios|
|                                    |                                                             |
|                                    | ``-a`` Muestra valores para ficheros y directorios          |
|                                    |                                                             |
|                                    | ``-h`` Salida más legible                                   |
|                                    |                                                             |
|                                    | ``-b``,``-k`` Tamaños en bytes/KBytes                       |
|                                    |                                                             |
|                                    | ``-s`` Muestra sólo la ocupación total                      |
+------------------------------------+-------------------------------------------------------------+
| ``df [-h] [device | directorio]``  | Para comprobar el espacio usado por las distintas particiones montadas en el sistema|
|                                    |                                                             |
|                                    | ``-h`` Indica el tamaño                                     |
+------------------------------------+-------------------------------------------------------------+
|``fsck [options]sistem_de_archivos``| Comprobar y reparar errores en un sistema de archivos       | 
|                                    | contenidos en una partición (la particion deve estar desmontada)|
|                                    |                                                             |
|                                    | ``-A`` Chequea todo los sistemas de archivos establecidos en /etc/fstab|
|                                    |                                                             |
|                                    | ``-V`` Detalla las acciones realizadas por fsck.            |
|                                    |                                                             |
|                                    | ``-t``  sistema de archivos a comprobar. El valor por defecto es ext4.|
|                                    |                                                             |
|                                    | ``-f``  fuerza una comprobación del sistema de archivos, aunque el sistema parezca | 
|                                    |  correcto.                                                  | 
|                                    |                                                             |
|                                    | ``-p`` repara los errores encontrados automáticamente, sin  | 
|                                    | la intervención delusuario                                  |
|                                    |                                                             |
|                                    | ``-y`` responde “yes” automáticamente a todas las preguntas |
|                                    | interactivas de la orden fsck.                              |
+------------------------------------+-------------------------------------------------------------+
| ``sudo badblocks[opt]<partición>`` | Permite localizar y aislar los sectores/bloques defectuosos |
|                                    | de una unidad de disco                                      |
|                                    |                                                             |
|                                    | ``-s`` Mostrará el proceso con porcentajes                  |
|                                    |                                                             |
|                                    | ``-v`` Nos mostrará el número de errores                    |
|                                    |                                                             |
|                                    | ``-n`` Se intentarán recuperar esos sectores, pero también  |
|                                    | la información que estaba en ellos                          |
|                                    |                                                             |
|                                    | ``-f`` Fuerza la lectura y escritura en dispositivos que estén montados|
+------------------------------------+-------------------------------------------------------------+
| `` blkid``                         | Para comprobar el UUID de un disco duro                     |
+------------------------------------+-------------------------------------------------------------+
|``sudo e4defrag [-cv] <partición>`` | Para saber la cantidad de ficheros fragmentados se puede ejecutar el comando|
|                                    |                                                             |
|                                    |``-c`` Muestra un recuento de la fragmentación actual con    |
|                                    | respecto a la fragmentación ideal. Si se combina con la opción |
|                                    | v, lo muestra para cada archivo.                            |
|                                    |                                                             |
|                                    |``v`` Muestra los detalles de la operación                   |
+------------------------------------+-------------------------------------------------------------+



Redirecciones:
~~~~~~~~~~~~~~~
En general, todos los comandos y, en consecuencia, los procesos que se generan a partir
de ellos reciben la información mediante un flujo de entrada de información y los resultados
son enviados mediante un flujo de salida.Además, estos flujos de entrada o salida se
identifican por un número.

Por defecto, se asignan tres ficheros:
    -``stdin``  = 0,entrada estándar.(teclado)

    -``stdout`` = 1,salida estánda.(pantalla)

    -``stderr`` = 2,salida de errores estándar.(pantalla)

No obstante, no siempre es así, ya que el intérprete de comandos permite redirigir
estos flujos y muchos comandos pueden tomar la entrada o salida estándar de otros ficheros
u otros comandos. Para ello, se utilizan los redireccionamientos y las tuberías.

Tuberías
----------------
+------------------------------------+---------------------------------------------------------------+
| Tubería                            | Descripción                                                   |
+====================================+===============================================================+
| ``comando1 | comando2``            | Tomará la salida estándar de 1 y la enviará como entrada al 2 |
+------------------------------------+---------------------------------------------------------------+
| ``comando > fichero``              | Redirección de la salida estándar a un fichero.Si existe se   |
|                                    | sobrescribe la salida del comando,sino se crea.(1 = abajo).   |
| ``comando 1> fichero``             |                                                               |    
+------------------------------------+---------------------------------------------------------------+
| ``comando >> fichero``             | Redirección de la salida estándar a un fichero.Si existe se   |
|                                    | añade la salida del comando,sino se crea(1 descriptor fichero)|
| ``comando 1>> fichero``            |                                                               |
+------------------------------------+---------------------------------------------------------------+
| ``comando < fichero``              | Redirección entrada de comando como fichero  en vez de teclado|
+------------------------------------+---------------------------------------------------------------+
| ``comando <<delimitador``          | Permite introducir texto hasta que se encuentre una línea     |
|                                    | únicamente con el delimitador establecido                     |
+------------------------------------+---------------------------------------------------------------+
| ``comando 2> fichero``             | Redirección de la salida de error estándar a un fichero.      |
|                                    | Si el fichero existe se sobreescribe, sino se crea.           |
+------------------------------------+---------------------------------------------------------------+
| ``comando 2>> fichero``            | Redirección de la salida de error estándar a un fichero.Si el |
|                                    | existe se añade la salida del comando(no borre), sino se crea.|
+------------------------------------+---------------------------------------------------------------+
| ``comando 2>/dev/null``            | Redirigimos cualquier flujo de información de la salida       |
|                                    | estándar o la de errores al dispositivo (que no lo muestre).  |
+------------------------------------+---------------------------------------------------------------+
| ``comando &> fichero``             | Redirección de la salida estándar y de la de error estándar al|
|                                    | mismo fichero el primero sustituye,el segundo añade contenido.|
| ``comando &>> fichero``            |                                                               |
+------------------------------------+---------------------------------------------------------------+
| ``comando 1>&2``                   | Redirigimos la salida estándar a la salida de error estandar  |
|                                    |                                                               |
| ``comando 2>&1``                   | y viceversa                                                   |
+------------------------------------+---------------------------------------------------------------+

Procesamiento de textos :
------------------------------------

- Grep
~~~~~~~~~~~~~~~

Para extraer información, localizando un patrón en uno o varios ficheros, mostrando las líneas donde se encuentra. 

.. code-block:: xml

 <grep [-nvicwr] patrón fichero_texto>

    • i: elimina la distinción entre mayúsculas y minúsculas
    • c: muestra el número de líneas totales que cumplen con el patrón para cada fichero
    • w: localiza el patrón como palabra completa y no como parte de una cadena de texto
    • n: imprime el número de línea del patrón localizado
    • v: busca líneas que no contengan el patrón especificado
    • r: búsqueda recursiva en el directorio

Además grep permite emplear expresiones regulares básicas (patrones que definen un conjunto de cadenas de texto)

    • . (punto): cualquier carácter, excepto el carácter fin de línea
    • *: indica que se puede repetir cero o más veces
    • +: indica que se puede repetir una o más veces
    • ?: indica que es opcional su aparicion
    • {n}: indica que se repite exactamente n veces
    • [lista]: coincide con algún carácter de la lista
    • [^lista]: no coincide con algún carácter de la lista
    • [caracter-caracter]:puede indicar rangos de caracteres al incluir guión
    • ^: comienzo de línea
    • $: fin de línea

- Cut
~~~~~~~~~~~~~~~

Para obtener información a partir de la división de un fichero o cadena de caracteres en columnas.

.. code-block:: xml

 <cut -c<lista_caracteres> -f<lista_columnas> [ -d<delimitador>] fichero_texto>

    • -c<lista_caracteres>: cortar por caracteres especificados por lista_caracteres.
    • -f<lista_columnas> [ -d<delimitador>]: corta por campos establecidos por
    lista_columnas. Por defecto, los delimitadores son: espacios, tabuladores o espacio
    fin de línea, a menos que se especifique otro mediante la opción -d.

Ejemplo:
    - Obtener el primer campo del fichero /etc/passwd : cut -f1 -d: /etc/passwd
    - Obtener los caracteres 1º,2º,3º,4º y 20º del fichero /etc/passwd : cut -c1-4,20 /etc/passwd

- Tr
~~~~~~~~~~~~~~~

El comando tr permite el reemplazo o eliminación de un conjunto de caracteres de la entrada estándar "stdin" y escribe el resultado en la salida estándar "stdout".

.. code-block:: xml

 <tr OPTION... SET1 [SET2]>


Un SET es básicamente una serie de caracteres que incluyen caracteres de escape especiales con barra invertida.

    • La opción -c usa el complemento de SET1. caracteres que no queremos que se vean afectados.
    • La opción -d permite eliminar los caracteres especificados en el SET1.
    • La opción -s reemplaza una secuencia de ocurrencias repetidas con el juego de caracteres en el último SET.
    • La opción -t obliga a que SET1 se trunque a la longitud de SET2 antes de realizar el procesamiento posterior. 

- Sort
~~~~~~~~~~~~~~~

Para mostrar, de forma ordenada, las líneas de un fichero.Las letras minúsculas tienen un orden mayor que las mayúsculas y sigue el ASCII. 

.. code-block:: xml

 <sort [-fnru] [-t <delimitador>] [-k <num_campo>] lista_archivos>

    • f: ignora las mayúsculas y las minúsculas
    • r: invierte el orden
    • n: ordena numéricamente en lugar de alfabéticamente
    • u: elimina las entradas repetidas
    • t: indica un delimitador o separador de campos
    • k: indica el número de campo por el que se va a realizar la ordenación.

- Find
~~~~~~~~~~~~~~~

Para localizar archivos en el sistema de archivos por diferentes criterios

.. code-block:: xml

 <find [ruta] -[criterio] [acción]>

- Criterios de busqueda:
    
Por nombre de fichero:
    •name patrón: buscar ficheros con patrones.
    
    •iname patrón: =que name perosin distinguir m de M.

Por nivel de profundidad en subdirectorios:
    •maxdepth n: especifica hasta qué subdirectorios se realiza la búsqueda. La ruta especificada se encuentra en el nivel 1, un subdirectorio dentro de este en el nivel 2 y así sucesivamente.
    
    •mindepth n: especifica desde qué nivel comienza la búsqueda.Como arriba pero de forma recursiba

Por tiempos de acceso, modificación y cambio:
    •Podemos hacer búsquedas atendiendo a la fecha de la última modificación del inodo (c),última modificación de su            contenido (m) y último acceso de su contenido (a). Para cualquiera de ellas, se puede especificar el tiempo en minutos (min) o en días (time).  Los valores númericos que acompañan a las opciones pueden ser: +n indicando mayor que, -n indicando menor que y n indicando igualdad. 

Por comparación de ficheros:
    •newer fichero: Busca archivos que hayan sido modificados más recientemente que el archivo especificado.
    
    •anewer fichero: Busca archivos a los que se haya accedido más recientemente que el archivo especificado haya sido            modificado.

    •cnewer fichero: Busca archivos cuyo estado de i-nodo haya sido modificado más recientemente que el archivo              especificado haya sido modificado.

Por tamaños:
     <-size [+-]n[bckMG]>
    •+n indica mayor que n, -n indica menor que n y n indica igualdad, siendo n un valor numérico.
    
    •b bloques de 512 bytes,c bytes,k kilobytes,M megabytes,G gigabytes
Por tipos de fichero:
    •type con alguno de los siguientes modificadores: l (enlace simbólico), d (directorio), f (fichero regular), b(dispositivo de tipo bloque) y c (dispositivo de tipo carácter). 

Por permisos:
    •-perm - o /

    •El signo "-" indica que el fichero debe contener al menos los permiso dados y "/" indica que debe tener alguno de los permisos que se dan. Si no se indica ninguno de estos dos signos, los permisos deben de ser idénticos a los especificados. 

Otros:
    • user usuario: localiza archivos por un usuario dado
    • inum inodo: busca ficheros por número de inodo
    • uid UID: busca ficheros por el UID de usuario
    • gid GID: busca ficheros por GID 

También podemos combinar opciones de búsqueda con criterio1 -and o -or criterio2 y -not o !criterio para negar.
Algunos casos requieren un procesamiento masivo de los archivos encontrados. Para ello, utilizamos el parámetro “-exec”, seguido de un comando Linux y sus parámetros. Todo el comando siempre se termina con el texto constante “{} \;”. Donde las llaves son el marcador de posición de los resultados que se ajustan a la búsqueda.

Con el comando stat puedo consultar información a detalle sobre archivos

- Tee
~~~~~~~~~~~~~~~

Por un lado, lee de la entrada estándar “stdin”, que se utiliza, por ejemplo, con el teclado
o un programa; por otro lado, emite lo que ha leído a través de la salida estándar “stdout”.

.. code-block:: xml

 <tee [OPTIONS] [FILE]>

comando du (disc usage) con opción -h (human readable) indica el espacio ocupado en un
formato comprensible

- Top
~~~~~~~~~~~~~~~
Se utiliza si en lugar de una instantánea de los procesos actuales del sistema, necesitamos una actualización continua de la información de los procesos del sistema, esto nos permite visualizar el estado del sistema, mostrando información de los procesos en tiempo real. 

..code-block:: xml

top  -  12:25:59up  46 min,  1 user,  load average:  0,05,  0,12,  0,17

Tareas:  218 total,  2 ejecutar,  216 hibernar,  0 dtener,  0 zombie

%Cpu(S):  3,1 usuario,  1,7 sist,  0,0 adecuado,  95,2 inact,  0,0 en espera

MiB Men :  1975,8 total,  247,3 libre,  844,3 usado,  884,2 buffer/caché

MiB Intercambio:  1162,4 total,  933,7 libre,  228,7 usado.  947,9 disponible

..

- Línea 1ª: hora actual, tiempo del sistema encendido, número de usuarios y carga media en intervalos de 1, 5 y 15 minutos, respectivamente.

- Línea 2ª: número de tareas, número de procesos en estado;

- Línea 3ª: tiempos de CPU de usuario, del kernel del sistema, etc.

- Línea 4ª: tamaño en MB de memoria física en total, libre, usada y utilizada por buffer.

- Línea 5ª: tamaño en MB de memoria virtual total, libre, usada.

- El resto de líneas muestran información de los procesos, identificando las columnas mediante cabeceras similares a las del comando ps.

    ejemplo:

    • Mostrar los procesos del usuario luis actualizando la información cada dos segundos:

    top -d 2 -u luis

    • Mostar información del proceso con PID 8933:

     top -p 8933


Particiones:
--------------

Cuando utilizamos una particion por comando hay diversas opciones a elegir 

Pulsamos la opción n para crear una nueva partición y vamos cubriendo los datos

    - Primero tendremos que indicar el tipo de partición, primaria o extendida; es decir escribimos p (primaria) o e (extendida)

    - Despues marcaremos el tamaño de la partición, que podremos especificar de dos formas:

      Con el número del último sector de la partición o con el tamaño en la forma +tamaño{K,M,G,T,P}. 

Con la opción p podremos ver la configuración de particiones realizada,antes de poder utilizar ninguna de estas particiones tenemos que:

    - Escribir la tabla de particiones a disco con la opción w

    - Formatear las particiones con el comando mkfs 


Usamos el comando lsblk sobre el disco /dev/sdc, dicho comando lee del archivo "sysfs" filesystem para obtener la información de discos y particiones.

    - ``f`` en el comando lsblk veo el tipo de sistema de ficheros utilizado

.. code-block:: xml

 sudo parted -l /dev/sdc 


Esto nos deja ver las particiones.

El paso final para poder leer y escribir de particiones es montarlas en una ruta del sistema de archivos

    - mount /dev/sdc5 /media/datos1 → Monta la partición 5 del disco /dev/sdc en la ruta /media/datos1. 

    - umount /dev/sdc5 → Desmonta la partición 5 del disco /dev/sdc de donde esté montada.


Los dispositivos /dev/loop* son como atajos que permiten acceder a archivos planos como si fueran dispositivos de almacenamiento. Se usan para montar archivos de imagen, pero son solo de lectura, por lo que no cambian de tamaño.
