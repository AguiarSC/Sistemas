COMANDOS DE LAS PRÁCTICAS
=========================

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


``cal``
-------

Muestra un calendario mensual. Su estructura básica es:

.. code-block:: sh

  cal
  cal -y 2024 -m 05 

..

El comando puede o no ir acompañado de los argumentos ``-y`` y ``-m``, siendo estos year (año) y month(mes), respectivamente. Entre sus opciones más comunes, destacan:

* ``-3``: muestra el mes actual junto con los meses anterior y siguiente.

  .. code-block:: sh

    cal -3

  ..


* ``-j``: muestra el número de día del año junto a cada día.

  .. code-block:: sh

    cal -j

  ..


* ``-m``: muestra un formato alternativo del calendario.

  .. code-block:: sh

    cal -m

  ..

* ``-h``: muestra la ayuda y una lista de todas las opciones.

  .. code-block:: sh

    cal -h

  ..



















