COMANDOS DE EDICIÓN, PROCESAMIENTO Y ESTADÍSTICAS DE ARCHIVOS, DIRECTORIOS O TEXTOS
===================================================================================

``awk``
-------

Es una herramienta de procesamiento de textos. Se utiliza principalmente para la manipulación y análisis de datos en formato de texto. Permite realizar operaciones de filtrado, formateo, y transformación de datos de manera eficiente. Presenta la siguiente estructura base:

.. code-block:: sh

  awk 'patrón {acción}' archivo

..

El ``patrón`` especifica cuándo debe ejecutarse la acción y puede ser una expresión regular o una condición lógica; ``la acción`` define qué operación se realizará en las líneas que coincidan con el patrón y están delimitadas por llaves {}.

Entre sus opciones más comunes, destacan:

* ``-F`` (field-separator): para definir el delimitador de campos. Por defecto, considera que están separados por espacios en blanco.

  .. code-block:: sh

    awk -F ',' '{print $1}' archivo.csv 

  ..

* ``-v``: para definir variables.

  .. code-block:: sh

    awk -v var=valor 'patrón {acción}' archivo

  ..

* ``-f``: para especificar un archivo que contiene el script awk a ejecutar.

  .. code-block:: sh

    awk -f script.awk archiv

  ..

Entre sus patrones más comunes y acciones comunes, destacan:

* ``%n``: hace referencia al n-ésimo campo de la línea actual.

  .. code-block:: sh

    awk '{print $1, $3}' archivo

  ..

* ``NR``: hace referencia al número de línea.

  .. code-block:: sh

    awk 'NR == 5' archivo

  ..

* ``$0``: hace referencia a la línea actual. Equivalente a ``cat archivo``

  .. code-block:: sh

    awk 'NR == 5' archivo

  ..

* Ejemplos de las prácticas

  .. code-block:: sh
  
    awk '/Linux/{count++} END{print count}' datos.txt

    Recorre cada línea del archivo datos.txt. Cada vez que encuentra una línea que contiene la palabra "Linux", 
    incrementa un contador (count). Al final del procesamiento de todas las líneas, imprime el valor del contador, 
    que representa el número total de líneas que contienen la palabra "Linux".Las comillas simples aseguran que la 
    expresión awk se pase como un solo argumento al comando awk. Además, protegen cualquier carácter especial dentro 
    del programa awk de ser interpretado por el shell antes de que awk tenga la oportunidad de procesarlo.
  
  ..


``cat``
-------

Se utiliza principalmente para concatenar y mostrar el contenido de archivos. Es una de las herramientas básicas y más usadas en la línea de comandos. Es muy útil y versátil, no solo para mostrar archivos sino también para combinarlos, crear nuevos archivos y más, mediante su uso combinado con redirección y pipes ``|``.

Entre sus opciones más comunes, destacan:

* ``cat archivo``: muestra el contenido de uno o más archivos en la salida estándar.

  .. code-block:: sh

    cat archivo.txt

  ..

* ``cat archivo1 archivo2 ...``: concatenar y muestra el contenido de varios archivos en la salida estándar.

  .. code-block:: sh

    cat archivo1.txt archivo2.txt

  ..

* ``cat > archivo``: crea un nuevo archivo o sobrescribe uno existente con la entrada que se proporcione desde el teclado hasta que se use ``Ctrl+D`` para indicar el fin de la entrada. A diferencia de ``cat < archivo`` que toma el contenido del archivo, sin crear ni sobreescribir, por lo que si no existe no har'a nada.

  .. code-block:: sh

    cat > nuevo_archivo.txt
    cat < END

  ..


* ``cat >> archivo``: redirige la salida estándar del comando cat hacia un archivo llamado "archivo.txt" pero, en este caso, en lugar de sobrescribir el archivo, añade el contenido al final del archivo existente. Si el archivo no existe, se crea. A diferencia de ``cat << archivo`` que inicia una construcción "here document", donde el texto introducido después de << (en este caso, "archivo.txt") se toma como el delimitador de fin de entrada. Esto permite al usuario escribir un bloque de texto directamente en la línea de comando o en un script de shell sin necesidad de un archivo de texto separado.

  .. code-block:: sh

    cat >> existente.txt
    cat << END

  ..

* ``cat -n archivo``: numera todas las líneas de los archivos proporcionados.

  .. code-block:: sh

    cat -n archivo.tx

  ..

* ``cat -b archivo``: numera solo las líneas no vacías.

  .. code-block:: sh

    cat -b archivo.txt

  ..

* ``cat -s archivo``: numera solo las líneas no vacías.

  .. code-block:: sh

    cat -s archivo.txt

  ..

* ``cat -v archivo``: muestra los caracteres no imprimibles, excepto las tabulaciones y saltos de línea, en un formato visible.

  .. code-block:: sh

    cat -v archivo.txt

  ..

* ``cat -e archivo``: equivalente a usar ``-vE``. Muestra los caracteres no imprimibles y marca el final de cada línea con un ``$``.

  .. code-block:: sh

    cat -e archivo.txt

  ..

* ``cat -t archivo``: equivalente a usar ``-vT``. Muestra los caracteres no imprimibles y reemplaza las tabulaciones con ``^I``.

  .. code-block:: sh

    cat -t archivo.txt

  ..

* Ejemplos de las prácticas

  .. code-block:: sh
  
    cat practicas/uno.texto > practicas/copiauno.texto

    Concatena el contenido del archivo "uno.texto" ubicado en el directorio "practicas".Toma ese contenido y lo 
    redirige hacia un nuevo archivo llamado "copiauno.texto", que también se encuentra en el directorio "practicas".
    Si el archivo "copiauno.texto" ya existe, se sobrescribirá con el nuevo contenido del archivo "uno.texto"
  
  ..


``cut``
-------

Se utiliza para extraer secciones específicas de archivos de texto. Sus opciones principales son:

* ``-c`` o ``--characters``: especifica los caracteres que se desean extraer.

  .. code-block:: sh

    cut -c1-5

  ..

* ``-d`` o ``--delimiter``: define el delimitador para separar los campos.

  .. code-block:: sh

     cut -d"," -f2

  ..

* ``-f`` o ``fields``: especifica los campos que se desean extraer.

  .. code-block:: sh

    cut -d"," -f1,3

  ..


* ``--complement``: complementa la selección; muestra lo que no se selecciona.

  .. code-block:: sh

    cut -d"," --complement -f2

  ..

* ``-b`` o ``--bytes``: especifica los bytes que se desean extraer.

  .. code-block:: sh

    cut -b1-5

  ..

* ``-n``: no dividir líneas; útil con -b para seleccionar bytes exactos sin dividir líneas.

  .. code-block:: sh

    cut -b1-5 -n

  ..

* ``--output-delimiter``: define el delimitador para la salida.

  .. code-block:: sh

    cut -d"," -f1,3 --output-delimiter="|"

  ..


* Ejemplos de las prácticas

  .. code-block:: sh
  
    cut -f1,2 -d, /tmp/users.csv > /tmp/users2.csv

    toma el archivo /tmp/users.csv, delimitado por comas, y extrae los campos 
    1 y 2, guardando los resultados en /tmp/users2.csv.
  
  ..

  .. code-block:: sh
  
    cut -f3 -d, users.txt | tail +2 | sort | uniq

    toma el archivo users.txt, delimitado por comas, extrae el tercer campo, ignora la primera 
    línea, ordena los resultados y muestra solo las líneas únicas a partir de la segunda.
  
  ..


``cp``
------

Se utiliza se utiliza para copiar archivos y directorios. Sus opciones principales son:

* ``-r`` o ``--recursive``: copiar directorios de forma recursiva

  .. code-block:: sh

    cp -r directorio_origen directorio_destino

  ..

* ``-p`` o ``--preserve``: conservar los atributos de los archivos copiados, incluyendo permisos de archivo, propietario, grupo, y las marcas de tiempo de acceso y modificación.

  .. code-block:: sh

    cp -p archivo_original destino

  ..

* ``-i`` o ``--interactive``: solicitar confirmación antes de sobrescribir un archivo existente.

  .. code-block:: sh

     cp -i archivo_origen archivo_destino

  ..

* ``-f`` o ``--force``: sobrescribir el archivo de destino sin solicitar confirmación, útil para automatizar tareas.

  .. code-block:: sh

    cp -f archivo_origen archivo_destino

  ..


* ``-u`` o ``--update``: copiar solo si el archivo de origen es más nuevo que el archivo de destino o si el archivo de destino no existe.

  .. code-block:: sh

    cp -u archivo_origen archivo_destino

  ..

* ``-v`` o ``--verbose``: mostrar detalles de la operación de copia.

  .. code-block:: sh

    cp -v archivo_origen archivo_destino

  ..

* ``-a`` o ``--archive``: copiar archivos y directorios de forma recursiva preservando permisos, propiedades y enlaces simbólicos.

  .. code-block:: sh

    cp -a directorio_origen directorio_destino

  ..

* Ejemplos de las prácticas

  .. code-block:: sh
  
    cp ./Ejercicio1/Texto1.txt ./Ejercicio1/Texto2.txt

    Duplica Texto1.txt con el nombre Texto2.txt dentro del mismo directorio.
  
  ..

  .. code-block:: sh
  
    cp ../Ejercicio1/Texto1.txt ./Tema1/Texto1.txt

    Copia Texto1.txt desde un directorio anterior a ./Tema1/Texto1.txt.
  
  ..


``touch``
---------

Se utiliza principalmente para crear archivos vacíos o actualizar las marcas de tiempo de archivos existentes. Sus opciones principales son:

* ``Crear un archivo vacío`` o ``actualizar la marca de tiempo de un archivo``

  .. code-block:: sh

    touch archivo.txt

    Esto creará un archivo vacío llamado archivo.txt en el directorio actual. Si archivo.txt ya existe,
    touch actualiza su marca de tiempo a la hora actual sin cambiar su contenido.

  ..

* ``Crear múltiples archivos de una vez``

  .. code-block:: sh

    touch archivo1.txt archivo2.txt archivo3.txt

  ..

* ``Especificar una marca de tiempo personalizada`` o ``-t``

  .. code-block:: sh

    touch -t 202401011200 archivo.txt

    Esto establece la marca de tiempo de archivo.txt al 1 de enero de 2024 a las 12:00 horas.

  ..

* ``Crear un archivo en un directorio específico``

  .. code-block:: sh

    touch /ruta/al/directorio/archivo.txt

    Esto crea un archivo llamado archivo.txt en el directorio especificado (/ruta/al/directorio/).

  ..

* ``Crear archivos con permisos específicos`` o ``-m``

  .. code-block:: sh

    touch -m archivo.txt

    Esto crea un archivo con permisos de lectura y escritura para el propietario, 
    pero sin permisos para el grupo y otros usuarios.

  ..

* Ejemplos de las prácticas

  .. code-block:: sh
  
    touch *?Hola\ caracola?*

    Utilizará touch junto con un patrón para crear archivos que coincidan con ese patrón.
    *: Este comodín coincide con cualquier cadena de caracteres de cualquier longitud.
    ?: Este comodín coincide con un solo carácter.
    \: Se utiliza para escapar el espacio en blanco en el patrón.
    "Hola\ caracola": Es el texto que debe coincidir exactamente.
    Por lo tanto, el comando creará archivos que contengan la cadena "Hola caracola" seguida 
    de un solo carácter antes y después de esta cadena en el directorio actual. Por ejemplo, 
    puede crear archivos como "xHola caracolay", "Hola caracolaZ", etc. Dependiendo de los 
    archivos que ya existan en el directorio y coincidan con este patrón.
  
  ..


``echo``
--------

Se utiliza para mostrar texto o variables en la salida estándar. Sus opciones principales son:

* ``Imprimir texto`` o ``imprimir variables``

  .. code-block:: sh

    echo "Hola, mundo!"

    nombre="Juan"
    echo "Hola, $nombre"

  ..

* ``Suprimir el salto de línea final`` o ``-n``

  .. code-block:: sh

    echo -n "Hola, mundo"
    Esto imprimirá "Hola, mundo" sin un salto de línea al final

  ..

* ``Imprimir texto con interpretación de escape de caracteres``

  .. code-block:: sh

    echo "Este es un texto con una nueva línea\nY esta es otra línea"

    Esto imprimirá "Este es un texto con una nueva línea\nY esta es otra línea" literalmente, 
    sin interpretar el carácter de nueva línea.

  ..

* ``Imprimir texto en color``

  .. code-block:: sh

    echo -e "\e[1;31m¡Error!\e[0m El archivo no se encontró."

    Esto imprimirá "¡Error!" en rojo, seguido de "El archivo no se encontró." en el color predeterminado del terminal.

  ..


``diff``
--------

Se utiliza para comparar el contenido de dos archivos línea por línea y mostrar las diferencias entre ellos. Sus opciones principales son:

* ``Comparar dos archivos``

  .. code-block:: sh

    diff archivo1.txt archivo2.txt

  ..

* ``Mostrar solo las diferencias`` o ``-q`` de ``--quiet``

  .. code-block:: sh

    diff -q archivo1.txt archivo2.txt

  ..

* ``Mostrar diferencias con contexto`` o ``-c`` de ``--context``

  .. code-block:: sh

    diff -c archivo1.txt archivo2.txt

    Esto mostrará las diferencias entre los archivos con contexto, mostrando 
    líneas adicionales alrededor de las diferencias para mayor claridad.

  ..

* ``Mostrar diferencias de forma unificadar`` o ``-u`` de ``--unified``

  .. code-block:: sh

    diff -u archivo1.txt archivo2.txt

    Esto mostrará las diferencias entre los archivos de forma unificada, que es más fácil de leer y entender.

  ..

* ``Ignorar los espacios en blanco`` o ``-b`` de ``--blank``

  .. code-block:: sh

    diff -b archivo1.txt archivo2.txt

    Esto mostrará las diferencias entre los archivos de forma unificada, que es más fácil de leer y entender.

  ..

* ``Ignorar mayúsculas y minúsculas`` o ``i`` de ``--ignore-case``

  .. code-block:: sh

    diff -i archivo1.txt archivo2.txt

  ..


``nano``
--------

Es un editor de texto simple y fácil de usar en sistemas Unix y Linux. Sus opciones principales son:

* ``Abrir un archivo``

  .. code-block:: sh

    nano archivo.txt

  ..

* ``Guardar un archivo``

  .. code-block:: sh

    Dentro del archivo: Ctrl + O

  ..

* ``Salir de nano``

  .. code-block:: sh

    Dentro del archivo: Ctrl + X

  ..

* ``Buscar y reemplazar``

  .. code-block:: sh

    Dentro del archivo: Ctrl + W

  ..

* ``Cortar, copiar y pegar``

  .. code-block:: sh

    Dentro del archivo: Ctrl + K para cortar texto, Ctrl + U para pegar texto y Ctrl + Shift + 6 para copiar texto.

  ..

* ``Numerar líneas``

  .. code-block:: sh

    Dentro del archivo: Alt + N

  ..


``mv``
------

Se utiliza para mover o renombrar archivos y directorios. Sus opciones principales son:

* ``Mover archivo o directorio a un nuevo destino``

  .. code-block:: sh

    mv archivo.txt /ruta/a/destino/
    mv archivo1.txt archivo2.txt /ruta/a/destino/

  ..

* ``Renombrar un archivo o directorio``

  .. code-block:: sh

    mv archivo_viejo.txt archivo_nuevo.txt
    mv directorio_viejo directorio_nuevo


  ..

* ``Sobreescribir un archivo de destino existente`` o ``-f`` de ``--force``

  .. code-block:: sh

    mv -f archivo.txt /ruta/a/destino/

    Esto moverá archivo.txt al directorio de destino y sobrescribirá cualquier archivo con el mismo nombre si ya existe.

  ..

* ``Solicitar confirmación antes de sobreescribir un archivo`` o ``-i`` de ``--interactive``

  .. code-block:: sh

    mv -i archivo.txt /ruta/a/destino/

    Esto moverá archivo.txt al directorio de destino, pero pedirá confirmación 
    si hay un archivo con el mismo nombre en el destino.

  ..


``tr``
------

Se utiliza para traducir o eliminar caracteres en un flujo de datos. Sus opciones principales son:

* ``Traducir caracteres``

  .. code-block:: sh

    echo "hello" | tr 'l' 'L'

    Esto cambiará todas las ocurrencias de 'l' por 'L', produciendo la salida "heLLo".

  ..

* ``Eliminar caracteres`` o ``-d`` de ``--delete``

  .. code-block:: sh

    echo "hello" | tr -d 'l'

    Esto eliminará todas las ocurrencias de 'l' en la entrada, produciendo la salida "heo".

  ..

* ``Traducir un rango de caracteres``

  .. code-block:: sh

    echo "12345" | tr '0-9' 'a-j'

    Esto cambiará cada dígito del 0 al 9 por una letra del alfabeto, produciendo la salida "abcdefghij".

  ..

* ``Sustituir un conjunto de caracteres por un único caracter``

  .. code-block:: sh

    echo "hola" | tr 'aeiou' '*'

    Esto cambiará todas las vocales por un asterisco, produciendo la salida "h*la".

  ..

* ``Capitalizar el texto``

  .. code-block:: sh

    echo "Hello" | tr 'A-Z' 'a-z'

    Esto convertirá todas las letras mayúsculas en minúsculas, produciendo la salida "hello".

  ..

* ``Eliminar caracteres no deseados utilizando conjuntos complementario``

  .. code-block:: sh

    echo "12345abcde" | tr -dc '0-9'

    Esto eliminará todos los caracteres excepto los dígitos, produciendo la salida "12345".

  ..

* Ejemplos de las prácticas

  .. code-block:: sh
  
    tr a z < /etc/passwd

    Todas las 'a' en el archivo serán cambiadas por 'z', resultando en un efecto de cifrado simple.

    tr -d ' ' < /etc/passwd

    Los espacios en blanco serán eliminados, dejando solo los caracteres restantes

    tr '[A-Z]' '[a-z]' < /etc/passwd

    Todas las letras en mayúsculas serán convertidas a minúsculas, manteniendo el resto del contenido del archivo.
  
  ..


``wc``
------

Se utiliza para contar palabras, líneas y caracteres en archivos o en la entrada estándar. Sus opciones principales son:

* ``Contar líneas`` o ``-l`` de ``--lines``

  .. code-block:: sh

    wc -l archivo.txt

  ..

* ``Contar palabras`` o ``-w`` de ``--words``

  .. code-block:: sh

    wc -w archivo.txt

  ..

* ``Contar caracteres`` o ``-c`` de ``--characters``

  .. code-block:: sh

    wc -c archivo.txt

  ..

* ``Mostrar todas las estadísticas y conteos de un archivo``

  .. code-block:: sh

    wc archivo.txt

  ..

* ``Contar en la entrada estándar``

  .. code-block:: sh

    echo "Hola Mundo" | wc

    Esto mostrará las líneas, palabras y caracteres en el texto "Hola Mundo" 
    que se proporciona a través de la entrada estándar.

  ..

* ``Contar la línea más larga``

  .. code-block:: sh

    wc -L archivo.txt

  ..



COMANDOS RELACIONADOS CON EL TIEMPO
===================================

``cal``
-------

Muestra un calendario mensual. Su estructura básica es:

.. code-block:: sh

  cal
  cal -y 2024 -m 05 
  El comando puede o no ir acompañado de los argumentos ``-y`` y ``-m``, 
  siendo estos year (año) y month(mes), respectivamente.

  cal -3
  Mostrará el mes actual junto con los meses anterior y siguiente.

  cal -j (--journal)
  Esto muestra el número de día del año junto a cada día.

  cal -m (--mode)
  Esto mostrará un formato alternativo del calendario

  cal -h (--help)
  Esto mostrará la ayuda y una lista de todas las opciones.

..


``date``
--------

Se utiliza para mostrar o establecer la fecha y la hora del sistema. Sus principales opciones son:

.. code-block:: sh

  date
  Mostrará la fecha y la hora actual en el formato predefinido.

  date "+%Y-%m-%d %H:%M:%S"
  Mostrará la fecha y la hora actual en el formato establecido: año-mes-día hora:minuto:segundo.

  date MMDDhhmmAA
  Esto establecerá la fecha y la hora del sistema. Por ejemplo, sudo date 052923002021 
  establecerá la fecha al 29 de mayo de 2021 a las 23:00.

  date -u
  Esto mostrará la fecha y la hora actuales en formato UTC (Tiempo Universal Coordinado).

  date "+%A, %B %d, %Y"
  Esto mostrará la fecha en un formato legible, por ejemplo, "Saturday, May 29, 2021".

..


``sleep``
---------

Se utiliza para hacer que el proceso actual espere durante un período de tiempo específico antes de continuar. Sus principales opciones son:

.. code-block:: sh

  sleep 5
  Esto hará que el proceso espere durante 5 segundos antes de continuar

  sleep 3m
  Esto hará que el proceso espere durante 3 minutos antes de continuar.

  sleep 1h
  Esto hará que el proceso espere durante 1 hora antes de continuar.

  sleep 1h30m15s
  Esto hará que el proceso espere durante 1 hora, 30 minutos y 15 segundos antes de continuar.

  sleep 0.5
  Esto hará que el proceso espere durante 0.5 segundos antes de continuar.

  Ctrl + C
  Esto interrumpirá el proceso de espera presionando en el terminal donde se ejecuta el comando.

..










COMANDOS RELACIONADOS CON LOS PERMISOS, SISTEMA O USUARIOS Y GRUPOS
===================================================================

``chmod``
---------

Se utiliza para cambiar los permisos de archivos y directorios. Sus opciones principales son:

* ``Por octal``. Véase conversión de permisos a octal en Gestión de ficheros.

  .. code-block:: sh

    chmod xyz archivo/directorio
    chmod 755 archivo

  ..

* ``Simbólicamente``. Véase conversión de permisos a simbólico en Gestión de ficheros.

  .. code-block:: sh

    chmod [ugoa] [+-=] [rwx] archivo/directorio
    chmod u+x archivo

  ..

* ``Por recursividad`` ``-R``. Se pueden modificar los permisos de manera recursiva en todos los archivos y directorios dentro del directorio especificado.

  .. code-block:: sh

    chmod -R 755 directorio

    El modificador -R indica que los cambios de permisos se aplicarán de forma recursiva a todos 
    los archivos y subdirectorios dentro del directorio directorio. Por lo tanto, todos los archivos
    y directorios dentro de directorio también recibirán permisos 755, asegurando que todos sean 
    accesibles y ejecutables según sea necesario.

  ..

* Ejemplos de las prácticas

  .. code-block:: sh
  
    chmod g-r agenda

    Quita el permiso de lectura (r) del grupo (g) para el archivo o directorio agenda.
  
  ..

  .. code-block:: sh
  
    chmod g-wx,o+r agenda

    Quita los permisos de escritura (w) y ejecución (x) del grupo (g) y agrega permiso 
    de lectura (r) para otros usuarios (o) al archivo o directorio agenda.
  
  ..

  .. code-block:: sh
  
    chmod u+x script.sh

    Agrega permiso de ejecución (x) al propietario (u) del archivo script.sh. 
    Esto permite al propietario ejecutar el script como un programa.
  
  ..
